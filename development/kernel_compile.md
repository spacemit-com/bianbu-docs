---
sidebar_position: 1
---

# 内核编译

下面以`linux-6.6`为例，介绍如何为Bianbu编译自己的内核。

## 下载源码

```shell
git clone https://gitee.com/bianbu-linux/linux-6.6 ~/linux-6.6
```

## 交叉编译

### 开发环境

参考Bianbu Linux的[开发环境](https://bianbu-linux.bianbu.xyz/download_and_build#%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83)准备好交叉编译环境。

### 编译器

地址：[http://archive.spacemit.com/toolchain/](http://archive.spacemit.com/toolchain/)

1. 下载交叉编译器，例如`spacemit-toolchain-linux-glibc-x86_64-v1.0.0.tar.xz`：

2. 解压：

   ```shell
   sudo tar -Jxf /path/to/spacemit-toolchain-linux-glibc-x86_64-v1.0.0.tar.xz -C /opt
   ```

3. 设置交叉编译器环境变量：

   ```shell
   export PATH=/path/to/spacemit-toolchain-linux-glibc-x86_64-v1.0.0/bin:$PATH
   ```

### 编译软件包

进入内核源码目录：

```shell
cd ~/linux-6.6
```

设置内核编译参数：

```shell
export CROSS_COMPILE=riscv64-unknown-linux-gnu-
export ARCH=riscv
export LOCALVERSION=""
```

生成默认配置：

```shell
make k1_defconfig
```

修改配置，不改可跳过：

```shell
make menuconfig
```

如需保存修改后的配置：

```shell
make savedefconfig
mv defconfig arch/riscv/configs/k1_defconfig
```

编译debian软件包：

```shell
make -j$(nproc) bindeb-pkg
```

当看到以下信息，说明编译成功。

```
dpkg-genchanges: info: binary-only upload (no source code included)
 dpkg-source --after-build .
dpkg-buildpackage: info: binary-only upload (no source included)
```

软件包位于上一层目录，常用包：

- linux-image-6.6.36_6.6.36-*.deb

  内核Image软件包。

- linux-tools-6.6.36_6.6.36-*.deb

  `perf`等工具软件包。

拷贝到设备，安装然后重启即可：

```shell
sudo dpkg -i linux-image-6.6.36_6.6.36-*.deb
sudo reboot
```

