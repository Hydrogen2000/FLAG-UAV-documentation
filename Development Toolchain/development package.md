# development package

开发用功能包配置汇总

## 一、plotjuggler

安装plotjuggler软件：

```bash
sudo apt-get install ros-noetic-plotjuggler
```

安装相关ROS支持，否则无法打开bag文件：

```bash
sudo apt-get install ros-noetic-plotjuggler-msgs ros-noetic-plotjuggler-ros
```

运行plotjuggler：

```bash
rosrun plotjuggler plotjuggler
```

## 二、VRPN

安装VRPN库

```bash
sudo apt install ros-noetic-vrpn
```

创建工作空间编译vrpn_client_ros包

```bash
mkdir vrpn_client_ros/src -p
cd vrpn_client_ros/src
catkin_init_workspace
git clone https://github.com/ros-drivers/vrpn_client_ros.git
cd ..
catkin_make
```

启动vrpn_client_ros节点

```bash
mkdir vrpn_client_ros/src -p
cd vrpn_client_ros/src
catkin_init_workspace
git clone https://github.com/ros-drivers/vrpn_client_ros.git
cd ..
catkin_make
```
