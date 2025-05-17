---
sidebar_position: 2
---

# Bianbu 2.1/2.2 ROOTFS Creation

## Environment Requirements

Host machine should be Ubuntu 20.04/22.14, with docker ce and qemu-user-static (8.0.4, customized version with Vector 1.0 support enabled by default) installed.

### Docker

For docker ce installation, refer to [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/).

### QEMU

1. Uninstall binfmt-support

   The customized qemu-user-static conflicts with binfmt-support because `/etc/init.d/binfmt-support` provided by binfmt-support is a traditional SysVinit startup script, while `/lib/systemd/system/systemd-binfmt.service` provided by the customized qemu-user-static is a systemd service unit file. `/etc/init.d/binfmt-support` will execute after `/lib/systemd/system/systemd-binfmt.service`, overriding the systemd settings.

   ```shell
   sudo apt-get purge binfmt-support
   ```

2. Download the customized qemu

   ```shell
   wget https://archive.spacemit.com/qemu/qemu-user-static_8.0.4%2Bdfsg-1ubuntu3.23.10.1_amd64.deb
   ```

3. Install the customized qemu

   ```shell
   sudo dpkg -i qemu-user-static_8.0.4+dfsg-1ubuntu3.23.10.1_amd64.deb
   ```

4. Register qemu-user-static to the kernel so that riscv binary files can be executed directly throughout the system (including containers)

   ```shell
   sudo systemctl restart systemd-binfmt.service
   ```

5. Verify if qemu-user-static is successfully registered

   ```shell
   wget https://archive.spacemit.com/qemu/rvv
   chmod a+x rvv
   ./rvv
   ```

   If you see the following output, the registration is successful.

   ```
   helloworld
   spacemit
   ```

## Prepare Base ROOTFS

1. Create a working directory

   ```shell
   mkdir ~/bianbu-workspace
   ```

2. Create and start a container

   ```shell
   docker run --privileged -itd -v ~/bianbu-workspace:/mnt --name build-bianbu-rootfs harbor.spacemit.com/bianbu/bianbu:latest
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

5. Configure environment variables for later use

   ```shell
   export BASE_ROOTFS_URL=https://archive.spacemit.com/bianbu-base/bianbu-base-24.04-base-riscv64.tar.gz
   export BASE_ROOTFS=$(basename "$BASE_ROOTFS_URL")
   export TARGET_ROOTFS=rootfs
   ```

6. Download

   ```shell
   wget $BASE_ROOTFS_URL
   ```

7. Extract to the specified directory

   ```shell
   mkdir -p $TARGET_ROOTFS && tar -zxpf $BASE_ROOTFS -C $TARGET_ROOTFS
   ```

8. Mount some system resources to the rootfs

   ```shell
   mount -t proc /proc $TARGET_ROOTFS/proc
   mount -t sysfs /sys $TARGET_ROOTFS/sys
   mount -o bind /dev $TARGET_ROOTFS/dev
   mount -o bind /dev/pts $TARGET_ROOTFS/dev/pts
   ```

## Essential Configurations

### Configure Repository Sources

1. First, set up environment variables for later use

   ```shell
   export REPO="archive.spacemit.com/bianbu"
   ```

   [Click to view v2.1 release notes](../release_notes/bianbu_2.1.md)

   [Click to view v2.2 release notes](../release_notes/bianbu_2.2.md)

2. Configure bianbu.sources

   - For version 2.1

   ```shell
   cat <<EOF | tee $TARGET_ROOTFS/etc/apt/sources.list.d/bianbu.sources
   Types: deb
   URIs: https://$REPO/
   Suites: noble/snapshots/v2.1 noble-security/snapshots/v2.1 noble-updates/snapshots/v2.1 noble-porting/snapshots/v2.1 noble-customization/snapshots/v2.1 bianbu-v2.1-updates
   Components: main universe restricted multiverse
   Signed-By: /usr/share/keyrings/bianbu-archive-keyring.gpg
   EOF
   ```

   - For version 2.2

   ```shell
   cat <<EOF | tee $TARGET_ROOTFS/etc/apt/sources.list.d/bianbu.sources
   Types: deb
   URIs: https://$REPO/
   Suites: noble/snapshots/v2.2 noble-security/snapshots/v2.2 noble-updates/snapshots/v2.2 noble-porting/snapshots/v2.2 noble-customization/snapshots/v2.2 bianbu-v2.2-updates
   Components: main universe restricted multiverse
   Signed-By: /usr/share/keyrings/bianbu-archive-keyring.gpg
   EOF
   ```

### Configure DNS

```shell
echo "nameserver 8.8.8.8" >$TARGET_ROOTFS/etc/resolv.conf
```

### Install Hardware-Related Packages

```shell
chroot $TARGET_ROOTFS /bin/bash -c "apt-get update"
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades upgrade"
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install initramfs-tools"
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install bianbu-esos img-gpu-powervr k1x-vpu-firmware k1x-cam spacemit-uart-bt spacemit-modules-usrload opensbi-spacemit u-boot-spacemit linux-generic"
```

### Install Meta-Packages

Different variants have different meta-packages:

- Minimal: bianbu-minimal
- Desktop: bianbu-desktop bianbu-desktop-zh bianbu-desktop-en bianbu-desktop-minimal-en bianbu-standard bianbu-development
- NAS: bianbu-nas
- Desktop Lite：bianbu-desktop-lite

Desktop, Desktop Lite, and NAS variants are all based on Minimal. It is recommended to install the Minimal meta-package first, then install the corresponding meta-packages.

- Minimal variant:

```shell
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install bianbu-minimal"
```

- Desktop variant:

```shell
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install bianbu-minimal"
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install bianbu-desktop bianbu-desktop-zh bianbu-desktop-en bianbu-desktop-minimal-en bianbu-standard bianbu-development"
```

- Desktop Lite variant:

Since the user setup program is not yet fully adapted, you need to manually create a user to enter the desktop environment.

Note: This variant is only supported in Bianbu 2.2.

```shell
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install bianbu-minimal"

chroot $TARGET_ROOTFS /bin/bash -c "apt-get -y install adduser"
chroot $TARGET_ROOTFS /bin/bash -c "adduser --gecos \"\" --disabled-password bianbu"
chroot $TARGET_ROOTFS /bin/bash -c "echo bianbu:bianbu | chpasswd"
chroot $TARGET_ROOTFS /bin/bash -c "usermod -aG adm,cdrom,sudo,plugdev bianbu"

chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install bianbu-desktop-lite"
```

Tip: After installing all packages, you can clean up the cache to reduce the final firmware size:

```shell
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get clean"
```

## Common Configurations

#### Configure Locale

```shell
chroot $TARGET_ROOTFS /bin/bash -c "apt-get -y install locales"
chroot $TARGET_ROOTFS /bin/bash -c "echo \"locales locales/locales_to_be_generated multiselect en_US.UTF-8 UTF-8, zh_CN.UTF-8 UTF-8\" | debconf-set-selections"
chroot $TARGET_ROOTFS /bin/bash -c "echo \"locales locales/default_environment_locale select zh_CN.UTF-8\" | debconf-set-selections"
chroot $TARGET_ROOTFS /bin/bash -c "sed -i 's/^# zh_CN.UTF-8 UTF-8/zh_CN.UTF-8 UTF-8/' /etc/locale.gen"
chroot $TARGET_ROOTFS /bin/bash -c "dpkg-reconfigure --frontend=noninteractive locales"
```

#### Configure Timezone

```shell
chroot $TARGET_ROOTFS /bin/bash -c "echo 'tzdata tzdata/Areas select Asia' | debconf-set-selections"
chroot $TARGET_ROOTFS /bin/bash -c "echo 'tzdata tzdata/Zones/Asia select Shanghai' | debconf-set-selections"
chroot $TARGET_ROOTFS /bin/bash -c "rm /etc/timezone"
chroot $TARGET_ROOTFS /bin/bash -c "rm /etc/localtime"
chroot $TARGET_ROOTFS /bin/bash -c "dpkg-reconfigure --frontend=noninteractive tzdata"
```

#### Configure Time Server

```shell
sed -i 's/^#NTP=.*/NTP=ntp.aliyun.com/' $TARGET_ROOTFS/etc/systemd/timesyncd.conf
```

#### Configure Password

```shell
chroot $TARGET_ROOTFS /bin/bash -c "echo root:bianbu | chpasswd"
```

#### Configure Network

- minimal

```shell
cat <<EOF | tee $TARGET_ROOTFS/etc/netplan/01-netcfg.yaml
network:
    version: 2
    renderer: networkd
    ethernets:
        end0:
            dhcp4: true
        end1:
            dhcp4: true
EOF
chroot $TARGET_ROOTFS /bin/bash -c "chmod 600 /etc/netplan/01-netcfg.yaml"
```

- desktop/desktop-lite

```shell
cat <<EOF | tee $TARGET_ROOTFS/etc/netplan/01-network-manager-all.yaml
# Let NetworkManager manage all devices on this system
network:
version: 2
renderer: NetworkManager
EOF
chroot $TARGET_ROOTFS /bin/bash -c "chmod 600 /etc/netplan/01-network-manager-all.yaml"
```

Note: Only configure the relevant file for your specific variant.

## Generate Partition Images

Note: After completing installation and configuration, unmount the filesystems first!

```shell
mount | grep "$TARGET_ROOTFS/proc" > /dev/null && umount -l $TARGET_ROOTFS/proc
mount | grep "$TARGET_ROOTFS/sys" > /dev/null && umount -l $TARGET_ROOTFS/sys
mount | grep "$TARGET_ROOTFS/dev/pts" > /dev/null && umount -l $TARGET_ROOTFS/dev/pts
mount | grep "$TARGET_ROOTFS/dev" > /dev/null && umount -l $TARGET_ROOTFS/dev
```

Generate UUIDs and write them to /etc/fstab

```shell
UUID_BOOTFS=$(uuidgen)
UUID_ROOTFS=$(uuidgen)
cat >$TARGET_ROOTFS/etc/fstab <<EOF
# <file system>     <dir>    <type>  <options>                          <dump> <pass>
UUID=$UUID_ROOTFS   /        ext4    defaults,noatime,errors=remount-ro 0      1
UUID=$UUID_BOOTFS   /boot    ext4    defaults                           0      2
EOF
```

Move boot to another directory to create bootfs and rootfs partitions separately

```shell
mkdir -p bootfs
mv $TARGET_ROOTFS/boot/* bootfs
```

Generate bootfs.ext4 and rootfs.ext4

```shell
mke2fs -d bootfs -L bootfs -t ext4 -U $UUID_BOOTFS bootfs.ext4 "256M"
mke2fs -d $TARGET_ROOTFS -L rootfs -t ext4 -N 524288 -U $UUID_ROOTFS rootfs.ext4 "2048M"
```

Now, you should see two partition images in your current directory: bootfs.ext4 and rootfs.ext4, which can be flashed to the board using fastboot.

## Create Firmware

See [Firmware Creation Guide](./image.md).
