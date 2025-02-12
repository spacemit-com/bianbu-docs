---
sidebar_position: 2
---

# Bianbu Desktop 2.0 Release Notes

Build from Ubuntu 24.04.1 sources.

Bianbu 2.1 source：

```
Types: deb
URIs: https://archive.spacemit.com/bianbu/
Suites: noble/snapshots/<version> noble-security/snapshots/<version> noble-porting/snapshots/<version> noble-customization/snapshots/<version>
Components: main universe restricted multiverse
Signed-By: /usr/share/keyrings/bianbu-archive-keyring.gpg
```

`<version>` should be replaced with a version number, such as v2.1. If you need to download the source code, please change `Types: deb` to Types: `deb deb-src`.

## v2.1

Release date: 2025-2-11

Bianbu Linux version: [v2.1](https://bianbu-linux.spacemit.com/en/release_notes/bl-v2.1.y#v21-release-note)

### Major Updates

**AI**

- ollama: Added spacemit-ollama-toolkit
- open-webui: Support for openwebui

**Display**

- img-gpu-powervr: Support for calling PVR GPU's OpenCL implementation via libOpenCL.so.1, fixed the issue of some PPT slides failing to play
- mutter: Fixed occasional black screen issue on the login interface

**Multimedia**

- GStreamer1.0: Added SPACEMIT_GST_DEBUG_DUMP_DOT_DIR debugging feature, supporting the generation of Pipeline Graphviz charts
- gst-plugins-base1.0: Optimized glsinkbin display frame rate
- gst-plugins-bad1.0: Added active frame dropping feature for spacemitsrc component, fixed the issue of spacemitsrc data not being hardware encoded
- FFmpeg: Support for adding watermarks after hardware decoding
- mpv: Fixed crash issue after unlocking the screen
- audacious: Fixed the issue of two dots appearing on the taskbar

**Applications**

- chromium-browser-stable: Fixed several issues, optimized startup speed
- chromium: Upgraded to version 131, hardware video decoding is temporarily not supported
- LibreOffice: Adjusted compilation optimization level to -O2, improved interaction smoothness
- GNOME: Disabled thumbnails, optimized transition animations
- xfwm4: Fixed window manager lag issue in software rendering mode
- zed: Added spacemit-code-forge
- plymouth: Fixed abnormal display issue on the startup screen after flashing

**Development Tools**

- llvm: Support for LLVM 19
- gcc-13: Support for zicbom_zicbop_zicboz_zicond_zfh_zfhmin extensions
- sysprof: Fixed the issue of call stack not being displayed
