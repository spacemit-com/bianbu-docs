---
sidebar_position: 2
---

# Bianbu 1.0 ROOTFS Create

## Environment Requirements

The host machine is recommended to be Ubuntu 20.04/22.04 with Docker CE and a custom version of qemu-user-static (8.0.4) installed, which has Vector 1.0 support enabled by default.

### Docker

For Docker CE installation, refer to [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/).

### QEMU

1. Remove `binfmt-support`

   The custom version of `qemu-user-static` conflicts with `binfmt-support` because `binfmt-support` provides a traditional SysVinit startup script `/etc/init.d/binfmt-support`, whereas the custom `qemu-user-static` provides a systemd unit file `/lib/systemd/system/systemd-binfmt.service`. The `/etc/init.d/binfmt-support` runs later, overriding the systemd settings.

   ```shell
   sudo apt-get purge binfmt-support
   ```

2. Download the custom qemu

   ```shell
   wget https://archive.spacemit.com/qemu/qemu-user-static_8.0.4%2Bdfsg-1ubuntu3.23.10.1_amd64.deb
   ```

3. Install the custom qemu

   ```shell
   sudo dpkg -i qemu-user-static_8.0.4+dfsg-1ubuntu3.23.10.1_amd64.deb
   ```

4. Register qemu-user-static with the kernel so that RISC-V binaries can be executed system-wide, including inside containers.

   ```shell
   sudo systemctl restart systemd-binfmt.service
   ```

5. Verify if qemu-user-static is registered successfully

   ```shell
   wget https://archive.spacemit.com/qemu/rvv
   chmod a+x rvv
   ./rvv
   ```

   If you see the following output, registration is successful:

   ```
   helloworld
   spacemit
   ```

## Prepare the Base RootFS

1. Create a working directory

   ```shell
   mkdir ~/bianbu-workspace
   ```

2. Create and start a container

   ```shell
   docker run --privileged -itd -v ~/bianbu-workspace:/mnt --name build-bianbu-rootfs ubuntu:24.04
   ```

3. Enter the container

   ```shell
   docker exec -it -w /mnt build-bianbu-rootfs bash
   ```

4. Install basic tools

   ```shell
   apt-get update
   apt-get -y install wget uuid-runtime
   ```

5. Set environment variables for ease of use in subsequent commands

   ```shell
   export BASE_ROOTFS_URL=https://archive.spacemit.com/bianbu-base/bianbu-base-23.10-base-riscv64.tar.gz
   export BASE_ROOTFS=$(basename "$BASE_ROOTFS_URL")
   export TARGET_ROOTFS=rootfs
   ```

6. Download

   ```shell
   wget $BASE_ROOTFS_URL
   ```

7. Extract to a specified directory

   ```shell
   mkdir -p $TARGET_ROOTFS && tar -zxpf $BASE_ROOTFS -C $TARGET_ROOTFS
   ```

8. Mount system resources into the rootfs

   ```shell
   mount -t proc /proc $TARGET_ROOTFS/proc
   mount -t sysfs /sys $TARGET_ROOTFS/sys
   mount -o bind /dev $TARGET_ROOTFS/dev
   mount -o bind /dev/pts $TARGET_ROOTFS/dev/pts
   ```

## Necessary Configuration

### Configure the Source Repositories

1. Set environment variables for ease of use in subsequent commands

   ```shell
   export DIST=mantic
   export REPO="archive.spacemit.com/bianbu-ports"
   export VERSION="v1.0.13"
   ```

2. Install the repository's GPG key

   ```shell
   wget -O $TARGET_ROOTFS/usr/share/keyrings/bianbu-archive-keyring-mantic.gpg https://archive.spacemit.com/bianbu-ports/bianbu-archive-keyring.gpg
   wget -O $TARGET_ROOTFS/etc/apt/trusted.gpg.d/bianbu-archive-keyring-mantic.gpg https://archive.spacemit.com/bianbu-ports/bianbu-archive-keyring.gpg
   ```

3. Configure `sources.list`

   ```shell
   cat <<EOF | tee $TARGET_ROOTFS/etc/apt/sources.list
   # $DIST
   deb https://$REPO/ $DIST/snapshots/$VERSION main universe multiverse restricted
   # deb-src https://$REPO/ $DIST/snapshots/$VERSION main universe multiverse restricted

   # $DIST-security
   deb https://$REPO/ $DIST-security/snapshots/$VERSION main universe multiverse restricted
   # deb-src https://$REPO/ $DIST-security/snapshots/$VERSION main universe multiverse restricted
   EOF
   ```

4. Configure `sources.list.d/bianbu.list`

   ```shell
   cat <<EOF | tee $TARGET_ROOTFS/etc/apt/sources.list.d/bianbu.list
   # $DIST-spacemit
   deb https://$REPO/ $DIST-spacemit/snapshots/$VERSION main universe multiverse restricted
   # deb-src https://$REPO/ $DIST-spacemit/snapshots/$VERSION main universe multiverse restricted

   # $DIST-porting
   deb https://$REPO/ $DIST-porting/snapshots/$VERSION main universe multiverse restricted
   # deb-src https://$REPO/ $DIST-porting/snapshots/$VERSION main universe multiverse restricted

   # $DIST-customization
   deb https://$REPO/ $DIST-customization/snapshots/$VERSION main universe multiverse restricted
   # deb-src https://$REPO/ $DIST-customization/snapshots/$VERSION main universe multiverse restricted
   EOF
   ```

5. Set package source priorities

   ```shell
   cat <<EOF | tee $TARGET_ROOTFS/etc/apt/preferences.d/bianbu
   Package: *
   Pin: release o=Spacemit, n=mantic-spacemit
   Pin-Priority: 1200

   Package: *
   Pin: release o=Spacemit, n=mantic-porting
   Pin-Priority: 1100

   Package: *
   Pin: release o=Spacemit, n=mantic-customization
   Pin-Priority: 1100
   EOF
   ```

### Configure DNS

```shell
echo "nameserver 8.8.8.8" >$TARGET_ROOTFS/etc/resolv.conf
```

### Install Hardware-Related Packages

```shell
chroot $TARGET_ROOTFS /bin/bash -c "apt-get -y install ca-certificates"
chroot $TARGET_ROOTFS /bin/bash -c "apt-get update"
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades upgrade"
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install initramfs-tools"
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install bianbu-esos img-gpu-powervr k1x-vpu-firmware k1x-cam spacemit-uart-bt spacemit-modules-usrload opensbi-spacemit u-boot-spacemit linux-image-6.1.15"
```

### Install Metapackage

Different variants have different metapackages:

- Minimal: `bianbu-minimal`
- Desktop: `bianbu-desktop`, `bianbu-desktop-zh`, `bianbu-desktop-en`, `bianbu-desktop-minimal-en`, `bianbu-standard`, `bianbu-development`
- NAS: `bianbu-nas`

Here's an example for creating the minimal variant:

```shell
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install bianbu-minimal"
```

## General Configuration

#### Configure Locale

```shell
chroot $TARGET_ROOTFS /bin/bash -c "apt-get -y install locales"
chroot $TARGET_ROOTFS /bin/bash -c "echo \"locales locales/locales_to_be_generated multiselect en_US.UTF-8 UTF-8, zh_CN.UTF-8 UTF-8\" | debconf-set-selections"
chroot $TARGET_ROOTFS /bin/bash -c "echo \"locales locales/default_environment_locale select zh_CN.UTF-8\" | debconf-set-selections"
chroot $TARGET_ROOTFS /bin/bash -c "sed -i 's/^# zh_CN.UTF-8 UTF-8/zh_CN.UTF-8 UTF-8/' /etc/locale.gen"
chroot $TARGET_ROOTFS /bin/bash -c "dpkg-reconfigure --frontend=noninteractive locales"
```

#### Configure Time Zone

```shell
chroot $TARGET_ROOTFS /bin/bash -c "echo 'tzdata tzdata/Areas select Asia' | debconf-set-selections"
chroot $TARGET_ROOTFS /bin/bash -c "echo 'tzdata tzdata/Zones/Asia select Shanghai' | debconf-set-selections"
chroot $TARGET_ROOTFS /bin/bash -c "rm /etc/timezone"
chroot $TARGET_ROOTFS /bin/bash -c "rm /etc/localtime"
chroot $TARGET_ROOTFS /bin/bash -c "dpkg-reconfigure --frontend=noninteractive tzdata"
```

#### Configure NTP Server

```shell
sed -i 's/^#NTP=.*/NTP=ntp.aliyun.com/' $TARGET_ROOTFS/etc/systemd/timesyncd.conf
```

#### Set Password

```shell
chroot $TARGET_ROOTFS /bin/bash -c "echo root:bianbu | chpasswd"
```

#### Configure Network (Optional)

If you only installed the minimal (`bianbu-minimal`) metapackage, network configuration should be done using Netplan:

```shell
cat <<EOF | tee $TARGET_ROOTFS/etc/netplan/01-netcfg.yaml
network:
    version: 2
    renderer: networkd
    ethernets:
        end0:
            dhcp4: true
EOF
chroot $TARGET_ROOTFS /bin/bash -c "chmod 600 /etc/netplan/01-netcfg.yaml"
```

## Generate Partition Images

Before proceeding to create the images, make sure to unmount all mounts:

```shell
mount | grep "$TARGET_ROOTFS/proc" > /dev/null && umount -l $TARGET_ROOTFS/proc
mount | grep "$TARGET_ROOTFS/sys" > /dev/null && umount -l $TARGET_ROOTFS/sys
mount | grep "$TARGET_ROOTFS/dev/pts" > /dev/null && umount -l $TARGET_ROOTFS/dev/pts
mount | grep "$TARGET_ROOTFS/dev" > /dev/null && umount -l $TARGET_ROOTFS/dev
```

Generate UUID and write to `/etc/fstab`:

```shell
UUID_BOOTFS=$(uuidgen)
UUID_ROOTFS=$(uuidgen)
cat >$TARGET_ROOTFS/etc/fstab <<EOF
# <file system>     <dir>    <type>  <options>                          <dump> <pass>
UUID=$UUID_ROOTFS   /        ext4    defaults,noatime,errors=remount-ro 0      1
UUID=$UUID_BOOTFS   /boot    ext4    defaults                           0      2
EOF
```

Move boot to another directory to create separate `bootfs` and `rootfs` partitions:

```shell
mkdir -p bootfs
mv $TARGET_ROOTFS/boot/* bootfs
```

Create `bootfs.ext4` and `rootfs.ext4`:

```shell
mke2fs -d bootfs -L bootfs -t ext4 -U $UUID_BOOTFS bootfs.ext4 "256M"
mke2fs -d $TARGET_ROOTFS -L rootfs -t ext4 -N 524288 -U $UUID_ROOTFS rootfs.ext4 "2048M"
```

At this point, you will have two partition images, `bootfs.ext4` and `rootfs.ext4`, which can be flashed to a board using `fastboot`.
