---
sidebar_position: 1
---

# Kernel Compile

Using `linux-6.6` as an example, we introduce how to compile your own kernel for Bianbu, supporting cross-compilation (fast) and local compilation (convenient).

## Download Source Code

```shell
git clone https://gitee.com/bianbu-linux/linux-6.6 ~/linux-6.6
```

## Cross Compilation

### Cross Development Environment

Refer to Bianbu Linux's [development environment](https://bianbu-linux.spacemit.com/source#%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83) to prepare the cross-compilation environment.

### Cross Compiler

URL: [http://archive.spacemit.com/toolchain/](http://archive.spacemit.com/toolchain/)

1. Download the cross-compiler, for example `spacemit-toolchain-linux-glibc-x86_64-v1.0.0.tar.xz`:

2. Extract:

   ```shell
   sudo tar -Jxf /path/to/spacemit-toolchain-linux-glibc-x86_64-v1.0.0.tar.xz -C /opt
   ```

3. Set the cross-compiler environment variables:

   ```shell
   export PATH=/opt/spacemit-toolchain-linux-glibc-x86_64-v1.0.0/bin:$PATH
   ```

### Cross Compile Kernel

Enter the kernel source directory:

```shell
cd ~/linux-6.6
```

Set kernel compilation parameters:

```shell
export CROSS_COMPILE=riscv64-unknown-linux-gnu-
export ARCH=riscv
export LOCALVERSION=""
```

Generate default configuration:

```shell
make k1_defconfig
```

Modify configuration, skip if not needed:

```shell
make menuconfig
```

To save the modified configuration:

```shell
make savedefconfig
mv defconfig arch/riscv/configs/k1_defconfig
```

Compile the Debian package:

```shell
make -j$(nproc) bindeb-pkg
```

When you see the following information, the compilation is successful.

```
dpkg-genchanges: info: binary-only upload (no source code included)
 dpkg-source --after-build .
dpkg-buildpackage: info: binary-only upload (no source included)
```

The packages are located in the parent directory, commonly used packages:

- linux-image-6.6.36_6.6.36-*.deb

  Kernel Image package.

- linux-tools-6.6.36_6.6.36-*.deb

  `perf` and other tool packages.

Copy to the device, install, and then reboot:

```shell
sudo dpkg -i linux-image-6.6.36_6.6.36-*.deb
sudo reboot
```

### Cross Compile Modules

To compile out-of-tree kernel modules, using rtl8852bs as an example, the general command is as follows:

```shell
cd /path/to/rtl8852bs
make -j$(nproc) -C ~/linux-6.6 M=/path/to/rtl8852bs modules
```

- Replace `/path/to/rtl8852bs` with your path

Clean:

```shell
make -j$(nproc) -C ~/linux-6.6 M=/path/to/rtl8852bs clean
```

### Cross Compile Device Tree

To compile the device tree separately:

```shell
make -j$(nproc) dtbs
```

## Local Compilation

You can directly compile the kernel on Bianbu, here is the guide.

### Local Development Environment

Install dependencies:

```shell
sudo apt-get install flex bison libncurses-dev debhelper libssl-dev u-boot-tools libpfm4-dev libtraceevent-dev asciidoc bc rsync libelf-dev devscripts
```

### Local Compile Kernel

Enter the kernel source directory:

```shell
cd ~/linux-6.6
```

Set kernel compilation parameters:

```shell
export ARCH=riscv
export LOCALVERSION=""
```

Generate default configuration:

```shell
make k1_defconfig
```

Modify configuration, skip if not needed:

```shell
make menuconfig
```

To save the modified configuration:

```shell
make savedefconfig
mv defconfig arch/riscv/configs/k1_defconfig
```

Compile the Debian package:

```shell
make -j$(nproc) bindeb-pkg
```

When you see the following information, the compilation is successful.

```
dpkg-genchanges: info: binary-only upload (no source code included)
 dpkg-source --after-build .
dpkg-buildpackage: info: binary-only upload (no source included)
```

The packages are located in the parent directory, commonly used packages:

- linux-image-6.6.36_6.6.36-*.deb

  Kernel Image package.

- linux-tools-6.6.36_6.6.36-*.deb

  `perf` and other tool packages.

Install and then reboot:

```shell
sudo dpkg -i linux-image-6.6.36_6.6.36-*.deb
sudo reboot
```

### Local Compile Modules

To compile out-of-tree kernel modules locally, you can do it without relying on the kernel source.

First, install `linux-headers`:

```shell
sudo apt-get install linux-headers-`uname -r`
```

Then compile the module, for example `rtl8852bs`:

```shell
cd /path/to/rtl8852bs
make -j$(nproc) -C /lib/modules/`uname -r`/build M=/path/to/rtl8852bs modules
```

- Replace `/path/to/rtl8852bs` with your path

Clean:

```shell
make -j$(nproc) -C /lib/modules/`uname -r`/build M=/path/to/rtl8852bs clean
```

## Other Components

### u-boot

Download the source code:

```shell
git clone https://gitee.com/bianbu-linux/uboot-2022.10 ~/uboot-2022.10
```

For cross-compilation, configure the following parameters first. Ignore for local compilation:

```shell
export PATH=/opt/spacemit-toolchain-linux-glibc-x86_64-v1.0.0/bin:$PATH
export CROSS_COMPILE=riscv64-unknown-linux-gnu-
export ARCH=riscv
```

Compile the Debian package:

```shell
cd ~/uboot-2022.10
VERSION=1~`git rev-parse --short HEAD`
dch --create --package u-boot-spacemit -v ${VERSION} --distribution mantic-porting --force-distribution 'Bianbu Test'
dpkg-buildpackage -us -uc -b
```

The generated Debian package is located in the parent directory. Install it using `dpkg` and reboot to take effect.

### opensbi

Download the source code:

```shell
git clone https://gitee.com/bianbu-linux/opensbi ~/opensbi
```

For cross-compilation, configure the following parameters first. Ignore for local compilation:

```shell
export PATH=/opt/spacemit-toolchain-linux-glibc-x86_64-v1.0.0/bin:$PATH
export CROSS_COMPILE=riscv64-unknown-linux-gnu-
```

Compile the Debian package:

```shell
cd ~/opensbi
VERSION=1~`git rev-parse --short HEAD`
dch --create --package opensbi-spacemit -v ${VERSION} --distribution mantic-porting --force-distribution 'Bianbu Test'
dpkg-buildpackage -us -uc -b
```

The generated Debian package is located in the parent directory. Install it using `dpkg` and reboot to take effect.
