---
slug: /
sidebar_position: 1
---

# Overview

**Bianbu** is a RISC-V optimized operating system based on **Ubuntu** community sources. It is designed for a wide range of product applications and delivers enhanced performance on RISC-V processors.

We provide the following Bianbu images for developers and customers to learn, test, and evaluate:

- **GNOME Desktop Version:** Built on GNOME Shell, it provides a GNOME desktop environment with pre installed applications such as Chromium, LibreOffice, MPV, etc. for system evaluation, demonstration, learning, and development.
- **LXQt Desktop Version:** A lightweight desktop version with a redesigned UI based on LXQt, designed for lightweight scenarios with high resource and performance requirements.
- **Minimal Version:** A non-graphical desktop environment for lightweight system development and evaluation.

## Why Bianbu?

- Provide developers with an operating system deeply optimized for RISC-V architecture processors
- Provide customers with system solutions to accelerate product mass production
- Drive the development of the RISC-V hardware and software ecosystem

## Vision

To empower every individual and every industry around the world with our technology and services.

## System Architecture

![](static/systemarch.png)

## Software Components

Bianbu is composed of the following key components:

- Applications
- Frameworks
- Runtimes
- Libraries
- Linux Kernel
- U-Boot
- OpenSBI

Bianbu manages the packages of these components through the [APT source](http://archive.spacemit.com/bianbu-ports/), and follow the standard Debian package format.

### Applications

- GNOME/LXQt desktop and its common applications
- Remote desktop
- Chromium browser
- LibreOffice suite
- Visual Studio Code
- Docker

### Frameworks

#### Application Frameworks

- Electron
- GTK
- Qt

#### Multimedia Frameworks

- FFmpeg (with Hardware Accelerated)
- GStreamer (with Hardware Accelerated)
- PipeWire

#### Inference Frameworks

- onnxruntime (with Hardware Accelerated)

### Runtimes

- Python
- Java
- Node.js
- Rust

### Libraries

- OpenCV (with RVV Accelerated)
- OpenSSL (with Hardware Accelerated)
- MPP (multimedia processing platform with C API and samples)
- Mesa 3D
- OpenGLES/Vulkan/OpenCL

### Linux Kernel

The Linux kernel is responsible for managing the processor and other hardware resources, providing an interface between users and applications and the hardware. Its main functions include: 
- Interrupt and clock management
- Process scheduling
- Memory management
- File system management
- Device driver management
- Network protocol stack

Supported versions:

- **6.1**: [https://gitee.com/bianbu-linux/linux-6.1](https://gitee.com/bianbu-linux/linux-6.1) (EOL)
- **6.6**:  [https://gitee.com/bianbu-linux/linux-6.6](https://gitee.com/bianbu-linux/linux-6.6) (LTS)

### U-Boot

U-Boot is a bootloader responsible for initializing specific hardware and loading the Linux kernel image, device tree, and initial RAM filesystem from media (such as SD card, eMMC, SPI Flash, SSD, network).

- Version: u-boot-2022.10
- Source code: [https://gitee.com/bianbu-linux/uboot-2022.10](https://gitee.com/bianbu-linux/uboot-2022.10)

### OpenSBI

OpenSBI is an implementation of the Supervisor Binary Interface for RISC-V architecture processors, running in M-mode firmware, providing interfaces for bootloaders, hypervisors, and operating systems to access hardware.

- Version: 1.3
- Source code: [https://gitee.com/bianbu-linux/opensbi](https://gitee.com/bianbu-linux/opensbi)

## Supported Devices

- BPI-F3
- Milk-V Jupiter
- MUSE Card
- MUSE Pi
- MUSE Pi pro
- MUSE Box
- MUSE Book

## Release Information

- **Bianbu 1.0** (End of Life)  
  Latest version: v1.0.15

- **Bianbu 2.x**  
  Latest version: v2.2.1

- **Bianbu 3.x**  
  Latest version: v3.0.1

## Feedback & Issues

Please report issues and suggestions via:  
[https://gitee.com/bianbu/bianbu-docs/issues](https://gitee.com/bianbu/bianbu-docs/issues).
