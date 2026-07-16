# development package

开发用软件包配置汇总

## 一、plotjuggler

安装 plotjuggler 软件包：

```bash
sudo apt-get install ros-noetic-plotjuggler
```

安装 ROS 支持软件包，否则无法打开 bag 文件：

```bash
sudo apt-get install ros-noetic-plotjuggler-msgs ros-noetic-plotjuggler-ros
```

运行 plotjuggler：

```bash
rosrun plotjuggler plotjuggler
```

## 二、VRPN

安装 VRPN ROS 软件包：

```bash
sudo apt install ros-noetic-vrpn
```

创建工作空间编译 vrpn_client_ros 功能包

```bash
mkdir vrpn_client_ros/src -p
cd vrpn_client_ros/src
catkin_init_workspace
git clone https://github.com/ros-drivers/vrpn_client_ros.git
cd ..
catkin_make
```

启动 vrpn_client_ros 节点

```bash
mkdir vrpn_client_ros/src -p
cd vrpn_client_ros/src
catkin_init_workspace
git clone https://github.com/ros-drivers/vrpn_client_ros.git
cd ..
catkin_make
```
