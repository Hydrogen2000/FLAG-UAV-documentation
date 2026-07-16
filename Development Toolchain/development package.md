# development package

开发用软件包配置汇总

## 一、git

安装 git 软件包：

```bash
sudo apt-get install git
```

只为 git 配置代理：*(以 v2rayA 代理端口为例)*

```bash
git config --global http.proxy http://127.0.0.1:20171
git config --global https.proxy https://127.0.0.1:20171
```

验证代理设置成功：

```bash
git config --get http.proxy
git config --get https.proxy
```

应该输出代理端口。

清除 git 代理：

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

## 二、plotjuggler

安装 plotjuggler 软件包：

```bash
sudo apt-get install ros-noetic-plotjuggler-ros
```

基于软件包依赖，会自动安装另外两个包 `ros-noetic-plotjuggler` 和 `ros-noetic-plotjuggler-msgs`。*(一些教程里提到，但不用单独安)*

运行 plotjuggler：

```bash
rosrun plotjuggler plotjuggler
```

## 三、VRPN

安装 VRPN 软件包：

```bash
sudo apt install ros-noetic-vrpn
```

创建工作空间，编译 vrpn_client_ros 功能包：

```bash
mkdir vrpn_client_ros/src -p
cd vrpn_client_ros/src
catkin_init_workspace
git clone https://github.com/ros-drivers/vrpn_client_ros.git
cd ..
catkin_make
```

启动 vrpn_client_ros 节点，如果预先填写 `sample.launch` 文件中的 `server: $(arg server)` 参数，直接使用以下指令：

```bash
cd vrpn_client_ros
source devel/setup.bash
roslaunch vrpn_client_ros sample.launch
```

如果 launch 文件没有预先修改，则指令最后一句需要添加参数：*(以 VRPN 发布端主机 IP 192.168.1.1 为例)*
```bash
roslaunch vrpn_client_ros sample.launch server:=192.168.1.1
```
