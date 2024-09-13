---
sidebar_position: 4
---

# JavaScript使用指南

## 准备工作

在使用JavaScript前，需要为其安装Node.js和npm。

### 使用apt安装Node.js


```shell
sudo apt-get update
sudo apt-get install -y nodejs
sudo apt-get install -y npm
```

检查是否安装成功。

```shell
$ node -v
v18.13.0
$ npm -v
9.2.0
```

bianbu源中的Node.js默认版本为v18.13.0，若想使用特定版本的Node.js，请使用NVM安装。


### 使用NVM安装特定版本Node.js

#### 安装NVM

根据 https://github.com/nvm-sh/nvm 提供的命令行下载并执行安装脚本，请根据该仓库替换最新的NVM版本号。

使用curl
```shell
sudo apt install curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```
或使用wget
```bash
sudo apt install wget
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

检查是否安装成功。

```shell
$ nvm -v
0.40.1
```

#### 安装Node.js

目前官方源中的node尚未适配riscv，直接安装会导致错误，因此我们从unofficial-builds中下载已适配riscv的node。  
更多信息请参考 https://github.com/nodejs/unofficial-builds/

```shell
NVM_NODEJS_ORG_MIRROR=https://unofficial-builds.nodejs.org/download/release nvm install 20.16.0
```

检查是否安装成功。

```shell
$ node -v
v20.16.0
```

### 示例

#### clumsy-bird

克隆demo项目。

```shell
git clone https://github.com/ellisonleao/clumsy-bird
```

安装依赖。

```shell
cd clumsy-bird
npm install
sudo apt install grunt
```

运行服务。

```shell
grunt connect
```

你可以看到如下输出，服务默认部署在 http://0.0.0.0:8001，在浏览器中打开该网页进行体验。

```shell
$ grunt connect
Running "connect:root" (connect) task
Waiting forever...
Started connect web server on http://0.0.0.0:8001
```

## Electron使用指南

### 准备工作

请参考JavaScript使用指南进行准备工作。

### 快速开始

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