---
sidebar_position: 1
---

# Bianbu Desktop 1.0更新说明

基于Ubuntu 23.10源码构建。

Bianbu 1.0源：

```
deb https://archive.spacemit.com/bianbu-ports/ mantic/snapshots/<version> main multiverse restricted universe
deb https://archive.spacemit.com/bianbu-ports/ mantic-security/snapshots/<version> main multiverse restricted universe
deb https://archive.spacemit.com/bianbu-ports/ mantic-spacemit/snapshots/<version> main multiverse restricted universe
deb https://archive.spacemit.com/bianbu-ports/ mantic-porting/snapshots/<version> main multiverse restricted universe
deb https://archive.spacemit.com/bianbu-ports/ mantic-customization/snapshots/<version> main multiverse restricted universe
```

`<version>`要替换成版本号，例如v1.0。

## v1.0更新说明

发布日期：2024-5-30

Bianbu Linux版本：[v1.0](https://bianbu-linux.spacemit.com/release_notes/bl-v1.0.y#v10%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)

### 主要组件

#### 应用

- GNOME 45.0
- Chromium 122
- Nautilus
- Shotwell
- LibreOffice
- mpv
- Rhythmbox
- docker.io 24.0.5

#### 应用框架

- Electron 29.3.1
- QT 5.15.10
- GTK 4.12.2

#### 多媒体框架

- FFmpeg 6.0 (with Hardware Accelerated)
- GStreamer 1.22.5 (with Hardware Accelerated)
- PipeWire 0.3.79

#### 推理框架

- onnxruntime 1.15.1 (with Hardware Accelerated)

#### 运行时

- Python 3.11.6
- OpenJDK 17 (default)
- Node.js

#### 库

- OpenCV 4.6.0
- OpenSSL 3.0.10
- MPP，进迭时空多媒体处理平台，提供 C API 和 sample
- Mesa 3D 22.3.5

### 已知问题

- 长时间挂起后无法唤醒

## v1.0.3

发布日期：2024-6-19

Bianbu Linux版本：[v1.0.3](https://bianbu-linux.spacemit.com/release_notes/bl-v1.0.y#v103%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)

### 主要更新

- 修复长时间挂起后无法唤醒
- 修复XFCE桌面卡顿的问题
- 修复文件浏览器属性对话框crash的问题
- 修复Chromium中文重复输入的问题

## v1.0.5

发布日期：2024-6-26

Bianbu Linux版本：[v1.0.5](https://bianbu-linux.spacemit.com/release_notes/bl-v1.0.y#v105%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)

### 主要更新

- 修复LibreOffice打开word或excel、保存文件低概率闪退的问题
- 修复茄子相机在系统休眠唤醒后无响应的问题

## v1.0.7

发布日期：2024-7-11

Bianbu Linux版本：[v1.0.7](https://bianbu-linux.spacemit.com/release_notes/bl-v1.0.y#v107%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)

## v1.0.8

发布日期：2024-7-16

Bianbu Linux版本：[v1.0.8](https://bianbu-linux.spacemit.com/release_notes/bl-v1.0.y#v108%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)

## v1.0.9

发布日期：2024-7-20

Bianbu Linux版本：[v1.0.9](https://bianbu-linux.spacemit.com/release_notes/bl-v1.0.y#v109%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)

## v1.0.11

发布日期：2024-8-1

Bianbu Linux版本：[v1.0.11](https://bianbu-linux.spacemit.com/release_notes/bl-v1.0.y#v1011%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)

## v1.0.12

发布日期：2024-8-2

Bianbu Linux版本：[v1.0.12](https://bianbu-linux.spacemit.com/release_notes/bl-v1.0.y#v1012%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)

### 主要更新

- 修复目标检测和姿态跟踪无法打开的问题

## v1.0.13

发布日期：2024-8-16

Bianbu Linux版本：[v1.0.13](https://bianbu-linux.spacemit.com/release_notes/bl-v1.0.y#v1013%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)

### 主要更新

- 支持开关机动画
- 支持安装`llm-client`大语言模型客户端
- 支持安装`box64`
- 完善universe组件
- 修复版本号错误，反复在线升级的问题

## v1.0.14

发布日期：2024-8-31

Bianbu Linux版本：[v1.0.14](https://bianbu-linux.spacemit.com/release_notes/bl-v1.0.y#v1014%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)

### 主要更新

- 修复HDMI作为主屏时，没接导致串口无法登录的问题
- 修复ssh不支持压缩的问题

## v1.0.15

发布日期：2024-9-7

Bianbu Linux版本：[v1.0.15](https://bianbu-linux.spacemit.com/release_notes/bl-v1.0.y#v1015%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E)

### 主要更新

- 修复spacemit-uart-bt软件包版本过低的问题
- 支持升级到Bianbu 2.0（开发中的版本）
