---
sidebar_position: 1
---

# Bianbu Desktop 1.0 Release Notes

## Bianbu 1.0 End of Life Announcement
SpacemiT Bianbu V1.0, which was built on Ubuntu 23.10, is no longer supported or updated by the Ubuntu community. SpacemiT has now released Bianbu V2.0 (currently at version V2.0.4), which is based on Ubuntu 24.04 and includes deep optimizations for RISC-V. Please note that Bianbu V1.0 is no longer maintained and has reached its End of Life (EOL).

**Bianbu 1.0 End of Life (EOL) Time: 2024/12/31**

## v1.0 release note

Release date: 2024-5-30

Bianbu Linux version: [v1.0](https://bianbu-linux.spacemit.com/en/release_notes/bl-v1.0.y#v10-release-note)

### Main components

#### Applications

- GNOME 45.0
- Chromium 122
- Nautilus
- Shotwell
- LibreOffice
- mpv
- Rhythmbox
- docker.io 24.0.5

#### Applications Framework

- Electron 29.3.1
- QT 5.15.10
- GTK 4.12.2

#### Multimedia Framework

- FFmpeg 6.0 (with Hardware Accelerated)
- GStreamer 1.22.5 (with Hardware Accelerated)
- PipeWire 0.3.79

#### Inference Framework

- onnxruntime 1.15.1 (with Hardware Accelerated)

#### Runtime

- Python 3.11.6
- OpenJDK 17 (default)
- Node.js

#### Libraries

- OpenCV 4.6.0
- OpenSSL 3.0.10
- MPP, SpacemiT multimedia processing platform, provides C API and sample
- Mesa 3D 22.3.5

### Know issue

- Unable to wake up after suspend for a long time

## v1.0.3

Release date: 2024-6-19

Bianbu Linux version: [v1.0.3](https://bianbu-linux.spacemit.com/en/release_notes/bl-v1.0.y#v103-release-note)

### Major Updates

- Fix the issue of unable to wake up after a long time of suspend
- Fix the lag issue in XFCE desktop
- Fix the crash of the properties dialog box in the file browser
- Fix the issue of repeated Chinese character input in Chromium

## v1.0.5

Release date: 2024-6-26

Bianbu Linux version：[v1.0.5](https://bianbu-linux.spacemit.com/en/release_notes/bl-v1.0.y#v105-release-note)

### Major Updates

- Fix the issue of LibreOffice crashing with a low probability when opening Word or Excel files or saving files
- Fix the issue of cheese becoming unresponsive after the system wakes up from suspend

## v1.0.7

Release date: 2024-7-11

Bianbu Linux version: [v1.0.7](https://bianbu-linux.spacemit.com/en/release_notes/bl-v1.0.y#v107-release-note)

## v1.0.8

Release date: 2024-7-16

Bianbu Linux version: [v1.0.8](https://bianbu-linux.spacemit.com/en/release_notes/bl-v1.0.y#v108-release-note)

## v1.0.9

Release date: 2024-7-20

Bianbu Linux version: [v1.0.9](https://bianbu-linux.spacemit.com/en/release_notes/bl-v1.0.y#v109-release-note)

## v1.0.11

Release date: 2024-8-1

Bianbu Linux version: [v1.0.11](https://bianbu-linux.spacemit.com/en/release_notes/bl-v1.0.y#v1011-release-note)

## v1.0.12

Release date: 2024-8-2

Bianbu Linux version: [v1.0.12](https://bianbu-linux.spacemit.com/en/release_notes/bl-v1.0.y#v1012-release-note)

### Major Updates

- Fix object detection and pose tracking startup failed issue

## v1.0.13

Release date: 2024-8-16

Bianbu Linux version: [v1.0.13](https://bianbu-linux.spacemit.com/en/release_notes/bl-v1.0.y#v1013-release-note)

### Major Updates

- Supports boot and shutdown animations
- Supports installation of the `llm-client` large language model client
- Supports installation of the `box64`
- Adds the universe component
- Fixes issues with incorrect version numbers and repeated online upgrades

## v1.0.14

Release date: 2024-8-31

Bianbu Linux version: [v1.0.14](https://bianbu-linux.spacemit.com/en/release_notes/bl-v1.0.y#v1014-release-note)

### Major Updates

- Fix serial can not login when HDMI as primary screen and not connected
- Fix ssh unsupport compress issue

## v1.0.15

Release date: 2024-9-7

Bianbu Linux version: [v1.0.15](https://bianbu-linux.spacemit.com/en/release_notes/bl-v1.0.y#v1015-release-note)

### Major Updates

- Fix the package version of spacemit-uart-bt issue
- Support upgrade to Bianbu 2.0 (in development currently)
