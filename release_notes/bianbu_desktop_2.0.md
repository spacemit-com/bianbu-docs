---
sidebar_position: 2
---

# Bianbu Desktop 2.0更新说明

基于Ubuntu 24.04源码构建。

当前状态：开发中。

Bianbu 2.0源：

```
Types: deb
URIs: https://archive.spacemit.com/bianbu/
Suites: noble/snapshots/<version> noble-security/snapshots/<version> noble-porting/snapshots/<version> noble-customization/snapshots/<version>
Components: main universe restricted multiverse
Signed-By: /usr/share/keyrings/bianbu-archive-keyring.gpg
```

`<version>`要替换成版本号，例如v2.0beta2。如需下载源码，请将`Types: deb`改成`Types: deb deb-src`。

## v2.0beta2

发布日期：2024-9-2

Bianbu Linux版本：[v2.0rc5](https://bianbu-linux.bianbu.xyz/release_notes/bl-v2.0.y/#v20rc5%E6%9B%B4%E6%96%B0%E8%AF%B4%E6%98%8E%E5%BC%80%E5%8F%91%E4%B8%AD)

### 主要更新

- 修复HDMI作为主屏时，没接导致串口无法登录的问题
- 修复ssh不支持压缩的问题
