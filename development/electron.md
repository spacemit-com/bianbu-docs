---
sidebar_position: 4
---

# Electron使用指南

## 准备工作

在使用Electron前，需要为其安装Node.js和NPM。

```shell
sudo apt-get update
sudo apt-get install npm
```

检查是否安装成功。

```shell
npm -v
```

## 快速开始

下载[electron-quick-start](https://github.com/electron/electron-quick-start.git)，

```shell
git clone https://github.com/electron/electron-quick-start.git ~/electron-quick-start
```

安装SpacemiT的Electron包，

```shell
cd ~/electron-quick-start
ELECTRON_MIRROR=http://archive.spacemit.com/electron/ electron_use_remote_checksums=1 npm install electron@29.3.1
```

启动应用，

```shell
npm start
```

当看到下面界面，表示成功。

![electron-quick-start](./static/electron-quick-start.png)