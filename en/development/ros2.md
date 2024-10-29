---
sidebar_position: 4
---

# ROS2 User Guide

Currently we only provide prebuilt tarballs.

## Use the prebuilt package

ROS2 we support is built on Bianbu 2.0, so to avoid unnecessary environment issues, please use Bianbu 2.0 to develop and use. prebuilt includes only all packages in the base version of ROS2, as described by the repository listed in the [ros2.repos](https://github.com/ros2/ros2/blob/jazzy/ros2.repos) file.

### Environment preparation

#### Setting the locale

Make sure you have a locale that supports UTF-8

```shell
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale  # verify settings
```

#### Installation Prerequisites

* Install ROS2 dependencies

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

* Install the system Python libraries

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

### Download the prebuilt package

* Go to [Publishing page](https://archive.spacemit.com/ros2/prebuilt)

* Download the latest package for Bianbu OS ROS2, in this case it is located at: ~/ros2-jazzy-linux-riscv64-20240920.tar.gz

**Tips**

> As versions iterate, there may be multiple download options for prebuilt packages, which may result in different filenames.

### Install the prebuilt package

* Decompressing packages

```shell
sudo mkdir -p /opt/ros2/jazzy_prebuild
cd /opt/ros2/jazzy_prebuild
sudo tar -xzvf ~/ros2-jazzy-linux-riscv64-20240920.tar.gz
```

This will install the prebuilt package's files to the current path (in this case /opt/ros2/jazzy_prebuild).

**Tips**

> When you use another ROS2 distribution, such as Humble, replace jazzy_prebuild with humble_prebuild in this example

The unzipped folder should look like this:

```shell
➜  jazzy_prebuild ls
bin            include           local_setup.ps1           _local_setup_util_sh.py  setup.bash  setup.zsh  tools
COLCON_IGNORE  lib               local_setup.sh            local_setup.zsh          setup.ps1   share
etc            local_setup.bash  _local_setup_util_ps1.py  opt                      setup.sh    src
```

## Try some examples

Use echo $0 to determine whether you're using zsh or bash, zsh is used in this example.

If you're using bash, replace all zsh with bash in the following examples, or you might get some runtime errors.

```shell
echo $0
-zsh # This line is output, please do not execute it
```

### Basic topic communication

Open a terminal anywhere, update ROS2's environment variables using the source command, and run the C++ talker:

```shell
source /opt/ros2/jazzy_prebuild/setup.zsh
ros2 run demo_nodes_cpp talker
```

In another terminal, update ROS2's environment variables using the source command, and then run Python listener:

```shell
source /opt/ros2/jazzy_prebuild/setup.zsh
ros2 run demo_nodes_py listener
```

You should see that the talker says it's Publishing messages, and the listener says I heard those messages.

This verifies that the C++ and Python apis are working correctly. Hooray!

**Tips**

> This does not have to be repeated if: source /opt/ros2/jazzy_prebuild/setup.zsh is already executed in the current terminal

### Start turtlesim

If you've opened a new terminal, don't forget to run: source /opt/ros2/jazzy_prebuild/setup.zsh

For this example, please launch the terminal from the desktop. The terminal connected with ssh will not pull up the turtlesim interface

To launch turtlesim, enter the following command into your terminal:

```shell
ros2 run turtlesim turtlesim_node
```

You should see the simulator window pop up with a random turtle in the middle

![alt text](static/ROS2-turtlesim.png)

In the terminal, under the command, you will see messages from the node:

```shell
[INFO] [1726820259.299762059] [turtlesim]: Starting turtlesim with node name /turtlesim
[INFO] [1726820259.366410375] [turtlesim]: Spawning turtle [turtle1] at x=[5.544445], y=[5.544445], theta=[0.000000]
```

Open a new terminal and source ROS 2 again.

Now you will run a new node to control the turtle in the first node:

```shell
ros2 run turtlesim turtle_teleop_key
```

Use the arrow keys on your keyboard to control the turtle. It will move around the screen, using its attached “pen” to draw the path it followed so far.

### Summary

See jazzy for more example tutorials[The Official Tutorial](https://docs.ros.org/en/jazzy/Tutorials.html)

Since you are using pre-compiled ROS2, please skip the steps to install ROS2 when you come across them.

If you are prompted for a missing package, consider compiling from the source package or contact us.
