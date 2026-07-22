# ROS Noetic

Ubuntu 20.04.6 LTS 操作系统安装 ROS Noetic

采用社区鱼香ROS的一键安装脚本，避免繁琐的官网安装步骤和网络连接问题。

## 1. 安装ROS

```bash
wget http://fishros.com/install -O fishros && . fishros
```

依次选择：**一键安装:ROS** -> **更换系统源再继续安装** -> **更换系统源并清理第三方源** -> **根据测速结果手动选择源**，选择一个软件镜像源 -> 选择ROS镜像源，**清华镜像源** -> **noetic(ROS1)** -> **noetic(ROS1)桌面版**。

***注意：ROS镜像源最好就选择清华源，中科大源在测试中出现话题频率莫名丢帧的问题***

运行 ROS master 验证安装完成:

```bash
roscore
```

应输出类似以下的信息：

```bash
started roslaunch server http://flag-NUC13ANKi7:37207/
ros_comm version 1.17.4


SUMMARY
========

PARAMETERS
 * /rosdistro: noetic
 * /rosversion: 1.17.4

NODES

auto-starting new master
process[master]: started with pid [30944]
ROS_MASTER_URI=http://flag-NUC13ANKi7:11311/

setting /run_id to 61820cbc-85a8-11f1-9744-e9a9bbb2170c
process[rosout-1]: started with pid [30954]
started core service [/rosout]
```

## 2. 配置rosdep

```bash
wget http://fishros.com/install -O fishros && . fishros
```

依次选择: **一键安装:rosdep** -> 选择pip源。

完成后运行更新：

```bash
rosdepc update
```

