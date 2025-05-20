---
sidebar_position: 3
---

# Bianbu 2.2 Release Notes

Built from Ubuntu 24.04.1 sources.

Bianbu 2.2 sources:

```
Types: deb
URIs: https://archive.spacemit.com/bianbu/
Suites: noble/snapshots/v2.2 noble-security/snapshots/v2.2 noble-updates/snapshots/v2.2 noble-porting/snapshots/v2.2 noble-customization/snapshots/v2.2 bianbu-v2.2-updates
Components: main universe restricted multiverse
Signed-By: /usr/share/keyrings/bianbu-archive-keyring.gpg
```

Using this source allows you to install packages released in subsequent 2.2.x versions (such as 2.2.1), which are stored in bianbu-v2.2-updates.
To download source code, change `Types: deb` to `Types: deb deb-src`.

## v2.2

Release date: 2025-5-9

Bianbu Linux version: [v2.2](https://bianbu-linux.spacemit.com/release_notes/bl-v2.2.y)

### Major Updates

**New Image - bianbu-desktop-lite**

- Based on lxqt 2.1.0
- Uses Wayland protocol by default
- lxqt-wayland-session: new shortcuts
  - ctrl + shift + 3: screenshot entire screen
  - ctrl + shift + 4: screenshot custom area
  - F11: toggle fullscreen for applications
  - Ctrl + Alt + ←/→: switch between left/right workspaces
  - logo + F1~F4: jump to specified workspace

**Display**

- wlroots:
  - Added real-time desktop frame rate display
  - Fixed issue where HDMI screen shows red lower half after hot-plugging in mirror mode

- raindrop: Fixed issue where secondary desktop and icons may disappear in dual-screen extended mode

**Multimedia**

- mpp: Fixed segment fault when multiple encoding occurs
- pipewire: Fixed crash when locking screen during screen recording
- gst-plugins-bad1.0:
  - Added feature for spacemitsrc plugin to exit actively during sleep
  - Added support for spacemitsrc to actively drop frames
  - Fixed issue where encoding could not exit for a long time
- mpv:
  - Added dmabuf-wayland display backend
  - Fixed tearing issue when playing 120fps videos
  - Fixed video freeze issue during aging test
- k1x-cam:
  - Added max96716_max96717_imx556 SerDes output feature
  - Added sc501ai output feature and completed ISP tuning
  - Added dual-channel CCIC raw dump feature
  - Fixed ov5647 abnormal exposure and high noise issue
  - Fixed dvdd_powen_cnt mismatch issue during power cycling

- ffmpeg:
  - Added feature to decode and output one frame per input frame
  - Adjusted some log levels

**Development Tools**

- gpiozero: Supports RV4B 40Pin interface

**AI**

- asr-llm: Supports integration of automatic speech recognition with large language models

**BSP**

- bianbu-esos: Adapted to v2.2 kernel; added related license information
