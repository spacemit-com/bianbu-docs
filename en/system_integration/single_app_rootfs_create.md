---
sidebar_position: 2
---

# Single Application ROOTFS Creation

This document describes how to customize a rootfs based on Bianbu minimal to run a single application based on the labwc display server.

## Environmental requirements and basic ROOTFS creation

For host environment preparation and basic ROOTFS creation, see [bianbu 2.1/2.2 ROOTFS creation](./bianbu_2.1_rootfs_create.md). After completing the basic configuration of ROOTFS (essential configuration and common configuration), you can proceed to the following Labwc configuration.

## Configure Labwc

When the desktop login manager is not needed, you can directly start labwc to provide the wayland display environment. The specific process is as follows:

1. Install labwc;
2. Configure getty@tty1.service to automatically log in to the specified user when the system starts;
3. Configure .bashrc / .zshrc in the user directory to start labwc after the user logs in;
4. Configure the autostart file in the labwc config folder to automatically start the application.

### Install labwc

```shell
chroot $TARGET_ROOTFS /bin/bash -c "apt-get update"
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades upgrade"
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install labwc"
```

### Configure getty@tty1.service

By modifying the configuration of getty@tty1.service, you can achieve automatic login of the specified user when the system starts. First, you need to modify the ExecStart of getty@tty1.service:

```shell
chroot $TARGET_ROOTFS /bin/bash -c "mkdir -p /usr/lib/systemd/system/getty@tty1.service.d"
chroot $TARGET_ROOTFS /bin/bash -c "cat > /usr/lib/systemd/system/getty@tty1.service.d/override.conf <<'EOF'
[Service]
ExecStart=
ExecStart=-/sbin/agetty --noclear --autologin root %I \$TERM
EOF"
```

### Configure .bashrc to automatically start labwc

By modifying the root user's shell (the default for the root user is bash) configuration file, labwc can be automatically started after the user logs in.

Add the labwc startup command at the end of /root/.bashrc and specify the labwc configuration folder as /root/.config/labwc:

```shell
chroot "$TARGET_ROOTFS" /bin/bash -c "echo 'labwc -C /root/.config/labwc' >> /root/.bashrc"
```

### Configure autostart

Here we take the self-starting glmark2-es2-wayland as an example.

First install glmark2-es2-wayland:

```shell
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install glmark2-es2-wayland"
```

Then modify the /root/.config/labwc/autostart file:

```shell
chroot "$TARGET_ROOTFS" /bin/bash -c "mkdir -p /root/.config/labwc"
chroot "$TARGET_ROOTFS" /bin/bash -c "touch /root/.config/labwc/autostart"
chroot "$TARGET_ROOTFS" /bin/bash -c "printf 'glmark2-es2-wayland >/dev/null 2>&1 &\n' > /root/.config/labwc/autostart"
```

If you want to set the wallpaper when labwc starts, you need to put the wallpaper file in the system directory of rootfs (such as /usr/share/wallpapers/wallpaper.png) and modify the /root/.config/labwc/autostart file. Here we take the wallpaper provided by the bianbu-wallpapers deb package as an example:

```shell
chroot "$TARGET_ROOTFS" /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get -y --allow-downgrades install bianbu-wallpapers swaybg"
chroot "$TARGET_ROOTFS" /bin/bash -c "printf 'swaybg -m fill -i /usr/share/backgrounds/SolidIsland-2.png >/dev/null 2>&1 &\n' >> /root/.config/labwc/autostart"
```

Tip: After installing all packages, you can clean up the cache to reduce the final firmware size:

```shell
chroot $TARGET_ROOTFS /bin/bash -c "DEBIAN_FRONTEND=noninteractive apt-get clean"
```

### Configure rc.xml

rc.xml is the core configuration file of labwc, which is used to define the behavior, shortcut keys, themes, window rules, etc. of the window manager. For specific configuration, see the official website of labwc:[https://github.com/labwc/labwc/blob/master/docs/rc.xml.all](https://github.com/labwc/labwc/blob/master/docs/rc.xml.all)。Here is a simple configuration of the /root/.config/labwc/rc.xml file to automatically maximize the window when opening glmark2-es2-wayland:

```shell
chroot "$TARGET_ROOTFS" /bin/bash -c "mkdir -p /root/.config/labwc"
chroot "$TARGET_ROOTFS" /bin/bash -c "cat > /root/.config/labwc/rc.xml <<'EOF'
<?xml version=\"1.0\"?>
<labwc_config>
  <windowRules>
    <windowRule identifier=\"glmark2-es2-wayland\" matchOnce=\"true\">
      <skipTaskbar>yes</skipTaskbar>
      <action name=\"ToggleMaximize\" />
      <action name=\"ToggleAlwaysOnTop\" />
    </windowRule>
  </windowRules>
</labwc_config>
EOF"
```

After completing the above configuration, the system can automatically log in to the root user and start glmark2-es2-wayland when it starts.

## Generate Partition Images

See the corresponding section of [bianbu 2.1/2.2 ROOTFS creation](./bianbu_2.1_rootfs_create.md).

## Create Firmware

See [Firmware Creation Guide](./image.md).
