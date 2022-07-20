# Plateau Robotique Doosan

## Pre-requisites

This stack is being tested on Ubuntu 20.04 and ROS Noetic. Follow [ROS install instruction tutorial](http://wiki.ros.org/noetic/Installation/Ubuntu) for installing ROS full edition manually. Otherwise, use the ```ros_install.sh``` script for unattended installation

```
wget https://raw.githubusercontent.com/drmateo/plato_robot_doosan/master/ros_install.sh && chmod 755 ros_install.sh && ./ros_install.sh noetic
```

Download the plato_robot_doosan workspace

```
git clone --recurse-submodules https://github.com/drmateo/plato_robot_doosan.git plato_robot_ws
```

Install dependencies for dossan-robot stack

```
sudo apt-get install ros-noetic-rqt* ros-noetic-moveit* ros-noetic-gazebo-ros-control ros-noetic-joint-state-controller ros-noetic-effort-controllers ros-noetic-position-controllers ros-noetic-ros-controllers ros-noetic-ros-control ros-noetic-joint-state-publisher-gui ros-noetic-joint-state-publisher
```

```
cd plato_robot_ws/src
rosdep install --from-paths doosan-robot --ignore-src --rosdistro noetic -r -y
```

Noetic distro does not support serial package, so you have to install it manually.

```
git clone https://github.com/wjwwood/serial.git
```

## Build

```
cd ~/plato_robot_ws
catkin_make
source ./devel/setup.bash
```

## Usage

Set up the IP address of the host PC in static mode using the following LAN:
    192.168.137.HOST_IP/24   gw   192.168.137.1

where the host PC address ```HOST_IP``` can be defined in the range [2, 254] avoiding 100 (reserved for the robot) and 52 (reserved for the robot desktop PC)

Example of usage:
```
roslaunch dsr_launcher dsr_moveit.launch mode:=real host:=192.168.137.100 port:=12345
```
