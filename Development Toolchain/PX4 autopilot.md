# PX4 autopilot

PX4 飞控固件开发

## 一、编译 PX4 飞控固件

以 v1.13.3 为例。

### 1. 下载 PX4 源码

由于 PX4 工程大，很容易下载一半网络中断，强烈建议使用**代理**。

网络顺畅的话，可以直接运行：

```bash
git clone https://github.com/PX4/PX4-Autopilot.git --branch v1.13.3
```

如果网络总中断，可以按照以下步骤，先只下载最新一次提交：

```bash
git clone https://github.com/PX4/PX4-Autopilot.git --branch v1.13.3 --depth 1
```

进入仓库不断补全之前的提交：

```bash
cd ~/PX4-Autopilot
git fetch --depth 1000
...
git fetch --unshallow 
```

`--depth` 参数按照网络状况选择，多次运行，逐渐增大，例如100 200 300...1000 2000 3000...

`--unshallow` 参数表示补全所有提交。

仓库补全后，再进行`git fetch`会显示 `对于一个完整的仓库，参数 --unshallow 没有意义`。

### 2. 下载 PX4 子模块

```bash
cd ~/PX4-Autopilot
git submodule update --init --recursive
```

一定保证子模块下载完成，没有报错，大部分固件编译失败原因都是子模块不全。

如果网络状况不佳，多尝试运行几次，子模块完整后指令应该**无输出**。

### 3. 修改 PX4 源码

### 4. 编译PX4固件

针对自己的飞控单元选择编译指令，本工程为 **Holybro Pixhawk 6C**，指令如下：

```bash
make px4_fmu-v6c_default
```

在编译过程中，会遇到缺少一些软件包而编译失败的问题，按照编译提示逐渐安装齐软件包即可。例如本工程遇到了：

```bash
ModuleNotFoundError: No module named 'menuconfig'
CMake Error at cmake/kconfig.cmake:6 (message):
  kconfiglib is not installed or not in PATH

CMake Error at CMakeLists.txt:235 (project):
  The CMAKE_C_COMPILER:
    arm-none-eabi-gcc
  is not a full path and was not found in the PATH.

Failed to import jinja2: No module named 'jinja2'

Failed to import jsonschema: No module named 'jsonschema'

Failed to import toml: No module named 'toml'

ModuleNotFoundError: No module named 'future'
```

依次运行了以下命令进行补全：

```bash
pip3 install kconfiglib
sudo apt install gcc-arm-none-eabi
pip3 install --user jinja2
pip3 install --user jsonschema
pip3 install --user toml
pip3 install future
```

## 二、安装 MAVROS

MAVROS 软件包通过 MAVLink 协议支持运算平台与飞控单元的 ROS 通信。

### 1. 安装软件包

```bash
sudo apt-get install ros-noetic-mavros ros-noetic-mavros-extras
```

### 2. 通过官方脚本安装 GeographicLib 库

```bash
wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh
sudo bash ./install_geographiclib_datasets.sh
```

## 三、安装 QGroundControl 地面站

QG C是 PX4 飞控固件支持的地面站调试软件。

### (1) 安装软件包依赖

```bash
sudo usermod -a -G dialout $USER
sudo apt-get remove modemmanager -y
sudo apt install gstreamer1.0-plugins-bad gstreamer1.0-libav gstreamer1.0-gl -y
sudo apt install libfuse2 -y
sudo apt install libxcb-xinerama0 libxkbcommon-x11-0 libxcb-cursor-dev -y
```

### (2) 下载软件并赋予运行权限

官网下载链接：https://d176tv9ibo4jno.cloudfront.net/latest/QGroundControl.AppImage

下载完成后，赋予软件运行权限：

```bash
chmod +x ./QGroundControl.AppImage
```

之后可以通过双击运行软件，或者运行`./QGroundControl.AppImage`。
