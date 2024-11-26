---
sidebar_position: 4
---

# ROS2使用指南

目前我们提供ROS2 Jazzy 和 ROS2 Humble 两个版本的prebuilt包，以及 ROS2 Jazzy 版本的deb安装包。如果您使用Jazzy版本，请从 deb 方式安装，Humble 版本请参考[安装prebuilt包](##使用prebuilt包)

## 从 deb 包安装

ROS2 Jazzy Jalisco 的 Deb 软件包目前可用于 Bianbu Destop 2.0

### 环境准备

#### 设置语言环境

确保您有一个支持UTF-8的区域设置

```shell
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale  # verify settings
```

#### 启用所需的存储库

您需要将 ROS2 apt 存储库添加到您的系统中。

```shell
sudo vim /etc/apt/sources.list.d/bianbu.sources
```

将 noble-ros 添加到Suites末尾，如下所示

```shell
Types: deb
URIs: http://archive.spacemit.com/bianbu/
Suites: noble/snapshots/v2.0rc2 noble-security/snapshots/v2.0rc2 noble-porting/snapshots/v2.0rc2 noble-customization/snapshots/v2.0rc2 noble-ros
Components: main universe restricted multiverse
Signed-By: /usr/share/keyrings/bianbu-archive-keyring.gpg
```

保存、退出。

#### 安装开发工具（可选）

如果您要构建ROS包或以其他方式进行开发，您还可以安装开发工具：

```shell
sudo apt update && sudo apt install ros-dev-tools
```

### 安装 ROS2

设置存储库后更新 apt 存储库缓存

```shell
sudo apt update
```

ROS2 软件包构建在经常更新的 Bianbu 系统上。始终建议您在安装新软件包之前确保系统是最新的

```shell
sudo apt upgrade
```

桌面安装（推荐），包含：ROS、RViz、demo、教程包等

```shell
sudo apt install ros-jazzy-desktop
```

ROS-Base 安装，包含：通信库、消息包、命令行工具。没有 GUI 工具

```shell
sudo apt install ros-jazzy-ros-base
```

安装额外的 RMW 实现（可选）

ROS2 使用的默认中间件是Fast DDS ，但可以在运行时替换中间件（RMW）。请参阅有关如何使用多个 RMW 的[指南](https://docs.ros.org/en/jazzy/How-To-Guides/Working-with-multiple-RMW-implementations.html)

### 设置环境

通过 source 以下文件来设置您的 ROS2 环境

```shell
source /opt/ros/jazzy/setup.zsh
```

如果您使用 bash ，请将 setup.zsh 替换成 setup.bash

### 尝试一些例子

如果您在上面安装了ros-jazzy-desktop ，您可以尝试一些示例

在一个终端中，source /opt/ros/jazzy/setup.zsh ，然后运行 ​​C++ talker

```shell
source /opt/ros/jazzy/setup.zsh
ros2 run demo_nodes_cpp talker
```

在另一个终端中，source /opt/ros/jazzy/setup.zsh，然后运行 ​​Python listener ：

```shell
source /opt/ros/jazzy/setup.zsh
ros2 run demo_nodes_py listener
```

您应该看到talker说它正在Publishing消息，而listener说I heard这些消息。这验证了 C++ 和 Python API 是否正常工作。

### 后续步骤

现在，您可以继续学习[官方教程和演示](https://docs.ros.org/en/jazzy/Tutorials.html)来配置您的环境，创建您自己的工作区和包，并学习 ROS 2 核心概念。


## 使用prebuilt包

我们支持的 ROS2 是在 Bianbu 2.0 上构建的，因此，为了避免不必要的环境问题，请您使用 Bianbu 2.0 来开发和使用。prebuilt仅包含了 ROS2 基础版本中的所有包，具体包含的包列表由此 [ros2.repos](https://github.com/ros2/ros2/blob/jazzy/ros2.repos) 文件中列出的仓库所描述。

### 环境准备

#### 设置语言环境

确保您有一个支持UTF-8的区域设置

```shell
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale  # verify settings
```

#### 安装先决条件

* 安装 ROS2 的依赖库

```shell
sudo apt-get install -y \
    libxml2-utils \
    libxrandr-dev \
    libyaml-cpp-dev \
    libyaml-dev \
    libassimp-dev \
    libbenchmark-dev \
    libzstd-dev \
    lttng-tools \
    pybind11-dev \
    pydocstyle \
    pyflakes3 \
    pyqt5-dev \
    shiboken2 \
    tango-icon-theme \
    uncrustify \
    liborocos-kdl-dev \
    libbullet-dev \
    libcurl4-openssl-dev \
    libeigen3-dev \
    libfreetype-dev \
    libgl1-mesa-dev \
    libglu1-mesa-dev \
    libgtest-dev \
    graphviz \
    libacl1-dev \
    libasio-dev \
    clang-format \
    google-mock \
    libsqlite3-dev \
    libssl-dev \
    libqt5svg5-dev \
    libshiboken2-dev \
    libpyside2-dev \
    liblttng-ctl-dev \
    liblttng-ust-dev \
    liblz4-dev \
    libxaw7-dev \
    curl \
    cppcheck \
    clang-format \
    libspdlog-dev \
    qt5-qmake \
    qtbase5-dev \
    libconsole-bridge-dev \
    libtinyxml2-dev \
    libopencv-dev
```

* 安装系统Python的依赖库

```shell
sudo apt-get install -y \
    python3-argcomplete \
    python3-babeltrace \
    python3-catkin-pkg \
    python3-empy \
    python3-flake8 \
    python3-flake8-builtins \
    python3-flake8-comprehensions \
    python3-flake8-docstrings \
    python3-flake8-import-order \
    python3-flake8-quotes \
    python3-jsonschema \
    python3-lark \
    python3-matplotlib \
    python3-mypy \
    python3-psutil \
    python3-pycodestyle \
    python3-pydot \
    python3-pygraphviz \
    python3-pykdl \
    python3-pyqt5 \
    python3-pyqt5.qtsvg \
    python3-pyside2.qtsvg \
    python3-pytest \
    python3-pytest-cov \
    python3-pytest-mock \
    python3-pytest-timeout \
    python3-sip-dev
```

### 下载prebuilt包

* 进入[发布页面](https://archive.spacemit.com/ros2/prebuilt)

* 下载 Bianbu OS ROS2 的最新软件包，在本示例中，它下载位于：~/ros2-jazzy-linux-riscv64-20240920.tar.gz

**提示**

> 随着版本的迭代，可能有多个prebuilt包的下载选项，这可能会导致文件名不同。

### 安装prebuilt包

* 解压软件包

```shell
sudo mkdir -p /opt/ros2/jazzy_prebuild
cd /opt/ros2/jazzy_prebuild
sudo tar -xzvf ~/ros2-jazzy-linux-riscv64-20240920.tar.gz
```

这会将prebuilt包的文件安装到当前路径（ 在本例中是 /opt/ros2/jazzy_prebuild ）

**提示**

> 当您使用其它 ROS2 的发行版时，例如 Humble，请将本示例中的 jazzy_prebuild 替换为任何您喜欢的名字，注意不要同名，以免新的安装错误覆盖了之前的文件。

解压完成后的文件夹应该如下所示：

```shell
➜  jazzy_prebuild ls
bin            include           local_setup.ps1           _local_setup_util_sh.py  setup.bash  setup.zsh  tools
COLCON_IGNORE  lib               local_setup.sh            local_setup.zsh          setup.ps1   share
etc            local_setup.bash  _local_setup_util_ps1.py  opt                      setup.sh    src
```

## 尝试一些例子

使用 echo $0 确定您使用的是zsh还是bash，本示例中使用的是 zsh。

如果您使用的是 bash，后续示例中的所有 zsh 请替换成 bash ，否则可能导致一些运行时错误。

```shell
echo $0
-zsh # 这一行是输出，请不要执行
```

### 基本话题通信

在任意位置打开一个终端，使用 source 命令更新 ROS2 的环境变量，然后运行 ​​C++ talker ：

```shell
source /opt/ros2/jazzy_prebuild/setup.zsh
ros2 run demo_nodes_cpp talker
```

在另一个终端中使用 source 命令更新 ROS2 的环境变量，然后运行 ​​Python listener ：

```shell
source /opt/ros2/jazzy_prebuild/setup.zsh
ros2 run demo_nodes_py listener
```

您应该可以看到 talker 说它正在 Publishing 消息，而 listener 说 I heard 这些消息。

这验证了 C++ 和 Python API 是否正常工作。万岁！

**提示**

> 当如果当前终端已经执行：source /opt/ros2/jazzy_prebuild/setup.zsh，则不必重复执行

### 小海龟

如果您新打开了一个终端，不要忘记执行：source /opt/ros2/jazzy_prebuild/setup.zsh

本示例请在桌面中启动终端运行，使用 ssh 连接的终端无法拉起 turtlesim 的界面

要启动turtlesim，请在终端中输入以下命令：

```shell
ros2 run turtlesim turtlesim_node
```

您应该可以看到模拟器窗口弹出，中间有一只随机的海龟

![alt text](static/ROS2-turtlesim.png)

在终端中的命令下，您将看到来自节点的消息：

```shell
[INFO] [1726820259.299762059] [turtlesim]: Starting turtlesim with node name /turtlesim
[INFO] [1726820259.366410375] [turtlesim]: Spawning turtle [turtle1] at x=[5.544445], y=[5.544445], theta=[0.000000]
```

在另一个终端运行一个新节点来控制第一个节点中的海龟：

```shell
ros2 run turtlesim turtle_teleop_key
```

使用键盘上的方向键来控制乌龟。它会在屏幕上移动，用它附带的“笔”画出它到目前为止所经过的路径。

### 小结

jazzy的更多的示例教程请参考[官方教程](https://docs.ros.org/en/jazzy/Tutorials.html)

由于使用的是预编译好的 ROS2 ，当您在官网教程中遇到安装 ROS2 的步骤时请先选择跳过。

如果提示缺少包，考虑从源码包编译或者联系我们。
