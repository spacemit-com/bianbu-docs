---
sidebar_position: 4
---

# Bianbu 3.0 Release Notes

Built based on **Ubuntu 25.04** source code.

Bianbu 3.0 Repository:

```
Types: deb
URIs: https://archive.spacemit.com/bianbu/
Suites: plucky/snapshots/v3.0 plucky-security/snapshots/v3.0 plucky-updates/snapshots/v3.0 plucky-porting/snapshots/v3.0 plucky-customization/snapshots/v3.0 bianbu-v3.0-updates
Components: main universe restricted multiverse
Signed-By: /usr/share/keyrings/bianbu-archive-keyring.gpg
```

- Using this repository allows installation of subsequent 3.0.x releases (such as 3.0.1), which are stored in `bianbu-v3.0-updates`.
- To download source code, change `Types: deb` to `Types: deb deb-src`.

## v3.0

**Release Date:** July 31, 2025

Corresponding **Bianbu Linux** version: [v2.2.6](https://bianbu-linux.spacemit.com/release_notes/bl-v2.2.y)

### Major Updates

**Toolchain**

- **gcc-14**: Default enabled extension instruction sets "--with-arch=rv64gc_zba_zbb_zbc_zbs_zicsr_zifencei" and "--with-tune=spacemit-x60"

**Factory Reset**

- **read-only-rootfs-config**: Added support for read-only root filesystem

**Display**

- **wlroots**: Fixed vulkan rendering failure when using drm render node
- **raindrop**: Fixed probabilistic disappearance of secondary screen desktop and icons in dual-screen extended mode
- **xwayland**: Added transparent conversion support from OpenGL to Vulkan via Zink

**Multimedia**

- **freerdp3**: Added rvv_YUV420ToRGB_8u_P3AC4R

- **mpp**:
  - Fixed yuv420p parameter exception
  - Fixed mpp function pointer variables having the same name as ffmpeg functions
- **pipewire**: Fixed the issue where audio output device automatically switches to HDMI after sleep/wake
- **mpv**:
  - Specified to use opengl rendering
  - Fixed video display issue in desktop-lite
- **ffmpeg**:
  - Added decoding support for DRM_FORMAT_YUV420 output
  - Fixed avcodec_send_packet failure and abnormal decoding exit

**Libraries**

- **zlib**
  - Fixed sigsegv
  - Optimized chunkcopy_rvv

**BSP**

- **bianbu-esos**: Support for low memory solutions
