---
sidebar_position: 2
---

# Bianbu Desktop 2.0 Release Notes

Build from Ubuntu 24.04 sources.

Current status: in development.

Bianbu 1.0 source：

```
Types: deb
URIs: https://archive.spacemit.com/bianbu/
Suites: noble/snapshots/<version> noble-security/snapshots/<version> noble-porting/snapshots/<version> noble-customization/snapshots/<version>
Components: main universe restricted multiverse
Signed-By: /usr/share/keyrings/bianbu-archive-keyring.gpg
```

`<version>` should be replaced with a version number, such as v2.0beta2. If you need to download the source code, please change `Types: deb` to Types: `deb deb-src`.

## v2.0beta2

Release date: 2024-9-2

Bianbu Linux version: [v2.0rc5](https://bianbu-linux.spacemit.com/en/release_notes/bl-v2.0.y#v20rc5-release-note)

### Major Updates

- Fix serial can not login when HDMI as primary screen and not connected
- Fix ssh unsupport compress issue

## v2.0rc1

Release date: 2024-9-7

Bianbu Linux version: [v2.0rc6](https://bianbu-linux.spacemit.com/en/release_notes/bl-v2.0.y#v20rc6-release-note)

### Major Updates

- Support python3-gpiozero
- Support code-server
- Support apport
- gnome-initial-setup support set hostname

## v2.0rc2

Release date: 2024-9-30

Bianbu Linux version: [v2.0rc7](https://bianbu-linux.spacemit.com/en/release_notes/bl-v2.0.y#v20rc7-release-note)

### Major Updates

- Fix the issue of Chromium crashing when playing videos
- Fix the issue of Chromium cookies becoming invalid
- Update box64 to support RVV and running WPS Office

## v2.0

Release date: 2024-10-22

Bianbu Linux version: [v2.0](https://bianbu-linux.spacemit.com/en/release_notes/bl-v2.0.y#v20-release-note)

### Major Updates

- Fix the issue of "Failed to start plymouth-quit-wait" prompt on first startup
- Fix the status bar color issue in light theme
- Upgrade LLVM 18 to 18.1.8
- Upgrade GCC 14 to 14.2
- Update img-gpu-powervr to fix the gnome-shell compilation error
