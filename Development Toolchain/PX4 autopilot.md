## 4. 下载并编译PX4固件

### (1) 配置git和代理

由于PX4源码工程很大，网络连接不稳定很难成功，一定要**科学上网**！

下载git软件包：

```bash
sudo apt-get install git
```

配置git代理，本文的代理端口是`127.0.0.1:7890`：

```bash
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy https://127.0.0.1:7890
```

验证代理设置成功，运行以下指令，应该输出代理端口：

```bash
git config --get http.proxy
git config --get https.proxy
```

如果要取消代理，运行：

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

### (2) clone PX4 v1.13.3源码

网络顺畅的话，可以直接运行：
```bash
git clone https://github.com/PX4/PX4-Autopilot.git --branch v1.13.3
```

如果仍然因为源码工程太大，clone过程会中断，可以按照以下步骤，先只clone最新的一次提交：

```bash
git clone https://github.com/PX4/PX4-Autopilot.git --branch v1.13.3 --depth 1
```

进入仓库不断补全之前的提交，`--depth`后面的参数按照网络情况选择，逐渐增大，例如100 200 300...1000 2000 3000...，而`--unshallow`参数表示补全所有提交：
```bash
cd PX4-Autopilot/
git fetch --depth 1000
...
git fetch --unshallow 
```

仓库补全后，再进行`fetch`则会显示`对于一个完整的仓库，参数 --unshallow 没有意义`。

### 3. 下载PX4子模块

```bash
git submodule update --init --recursive
```

一定要保证这一步运行完成，如果有因为网络连接问题的`fatal`报错，多尝试运行几次。

### 4. 编译PX4固件

针对自己的飞控硬件选择编译命令，本文为`Holybro Pixhawk 6c`，运行命令如下：

```bash
make px4_fmu-v6c_default
```

编译时注意确认第一行的提示版本为`-- PX4 version: v1.13.3`。

在编译过程中，会遇到缺少一些软件包而编译失败的问题，按照编译提示逐渐安装齐软件包即可。例如本文遇到了：

```bash
Traceback (most recent call last):
  File "<string>", line 1, in <module>
ModuleNotFoundError: No module named 'menuconfig'
CMake Error at cmake/kconfig.cmake:6 (message):
  kconfiglib is not installed or not in PATH
  please install using "pip3 install kconfiglib"
```

```bash
CMake Error at CMakeLists.txt:235 (project):
  The CMAKE_C_COMPILER:
    arm-none-eabi-gcc
  is not a full path and was not found in the PATH.
  Tell CMake where to find the compiler by setting either the environment
  variable "CC" or the CMake cache entry CMAKE_C_COMPILER to the full path to
  the compiler, or to the compiler name if it is in the PATH.
-- Enabling double FP precision hardware instructions
```

```bash
Failed to import packaging: No module named 'packaging'
You may need to install it using:
    pip3 install --user packaging
```

```bash
Failed to import jinja2: No module named 'jinja2'
You may need to install it using:
    pip3 install --user jinja2
```

```bash
Failed to import toml: No module named 'toml'
You may need to install it using:
    pip3 install --user toml
```

```bash
Failed to import jsonschema: No module named 'jsonschema'
You may need to install it using:
    pip3 install --user jsonschema
```

```bash
Traceback (most recent call last):
  File "/home/hydrogen/PX4-Autopilot/src/drivers/uavcan/libuavcan/libuavcan/dsdl_compiler/libuavcan_dsdlc", line 59, in <module>
    from libuavcan_dsdl_compiler import run as dsdlc_run
  File "/home/hydrogen/PX4-Autopilot/src/drivers/uavcan/libuavcan/libuavcan/dsdl_compiler/libuavcan_dsdl_compiler/__init__.py", line 18, in <module>
    from dronecan import dsdl
ModuleNotFoundError: No module named 'dronecan'
```

```bash
Traceback (most recent call last):
  File "/home/hydrogen/PX4-Autopilot/src/modules/mavlink/mavlink/pymavlink/tools/mavgen.py", line 16, in <module>
    from pymavlink.generator import mavgen
  File "/home/hydrogen/PX4-Autopilot/src/modules/mavlink/mavlink/pymavlink/generator/mavgen.py", line 26, in <module>
    from future import standard_library
ModuleNotFoundError: No module named 'future'
```

依次运行了以下命令进行补全：

```bash
pip3 install kconfiglib
apt install gcc-arm-none-eabi
pip3 install --user packaging
pip3 install --user jinja2
pip3 install --user toml
pip3 install --user jsonschema
pip3 install dronecan
pip3 install future
