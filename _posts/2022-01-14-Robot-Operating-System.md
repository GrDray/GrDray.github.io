---
layout: post
title: 機器人作業系統
author: [Richard Kuo]
category: [Lecture]
tags: [jekyll, ai]
---

The Robot Operating System(ROS) is a set of software libraries and tools that help you build robot applications.

---
## ROS Introduction
**Paper:** [A ROS2 based communication architecture for control in collaborative and intelligent automation systems](https://arxiv.org/abs/1905.09654)<br>
**ROS** is a collection of tools and libraries that aids robotics software development. Software is written in form of nodes that exchange messages using a transport layer called **TCPROS** based on standard TCP/IP sockets.

ROS has a centralized network configuration which means that there has to exist a running ROS master. 
The master takes care of naming and registration services so that other ROS nodes could find each other on the network
and communicate in a peer-to-peer fashion. Having a configuration where all nodes depend on a central ROS master
is not robust, especially if nodes in a network are distributed on several computers. 

To improve on this design limitation, developers of **ROS2** implemented Object Management Group’s standard **DDS** as the communication middleware considering it to be scalable, robust and well-proven in mission-critical systems.

![](https://images.deepai.org/converted-papers/1903.05850/figures/station.jpg)
An Automated Guided Vehicle (AGV) carrying a diesel truck engine and an autonomous mobile platform (MiR100) carrying kitted material to be assembled on an engine enter the Collaborative Robot Assembly Station. 
![](https://github.com/rkuo2000/Robotics/blob/gh-pages/images/ROS2%20high-level%20communication%20overview.png?raw=true)
<br>

There are several ways to organize nodes, hubs, messages and topics in a distributed ROS system. 
![](https://d3i71xaburhd42.cloudfront.net/402e1ddcb55d584722bbe32f67a87a905f64afb0/7-Figure3-1.png)
(a) Distributor and collector node aided hub oriented communication; (b) Direct hub oriented communication

**Multi-Hub system**<br>

![](https://d3i71xaburhd42.cloudfront.net/402e1ddcb55d584722bbe32f67a87a905f64afb0/7-Figure4-1.png)
(a) Direct node type oriented communication; (b) State collector hub aided node type oriented communication

**TurtleBot**<br>
![](https://github.com/rkuo2000/Robotics/blob/gh-pages/images/ROS%20Robot%20System%20Diagram.png?raw=true)
![](https://emanual.robotis.com/assets/images/platform/turtlebot3/overview/turtlebot3_with_logo.png)
[TurtleBot3 手冊](https://github.com/ROBOTIS-GIT/turtlebot3)<br>

---
### [ROS](https://www.ros.org/)
ROS is released as distributions, also called “distros”<br>
* ROS **Noetic Ninjemys** on Ubuntu Linux (Recommended for Latest ROS 1 LTS) [Install](http://wiki.ros.org/noetic/Installation/Ubuntu)
* ROS **Foxy Fitzroy** on Ubuntu Linux, macOS, or Windows 10 (Recommended for Latest ROS 2 LTS) [Install](https://docs.ros.org/en/foxy/Installation.html)
* ROS **Galactic Gechelone** on Ubuntu Linux, macOS, or Windows 10 (Recommended for Latest ROS 2) [Install](https://docs.ros.org/en/galactic/Installation.html)

[other distributions](https://docs.ros.org/)<br>
<table>
<tr>
<td>Noetic Ninjemys</td>
<td>Foxy Fitzroy</td>
<td>Galactic Gechelone</td>
</tr>
<tr>
<td><img width="200" height="200" src="https://www.ros.org/imgs/noetic.png"></td>
<td><img width="200" height="200" src="https://www.ros.org/imgs/foxy.png"></td>
<td><img width="200" height="200" src="https://www.ros.org/imgs/galactic.png"></td>
</tr>
</table>

### [ROS on DDS](https://design.ros2.org/articles/ros_on_dds.html)
The Data Distribution Service (DDS) for real-time systems is an [Object Management Group (OMG)](https://www.omg.org/) machine-to-machine (sometimes called middleware or connectivity framework) standard that aims to enable dependable, high-performance, interoperable, real-time, scalable data exchanges using a publish–subscribe pattern.

DDS addresses the needs of applications like aerospace and defense, air-traffic control, autonomous vehicles, medical devices, robotics, power generation, simulation and testing, smart grid management, transportation systems, and other applications that require real-time data exchange.

DDS has been used in:
* battleships
* large utility installations like dams
* financial systems
* space systems
* flight systems
* train switchboard systems

**[DDSI-RTPS](https://www.omg.org/spec/DDSI-RTPS/About-DDSI-RTPS/)**<br>
DDSI: DDS Interoperability Wire Protocol
RTPS: Real-Time Publish-Subscribe protocol
The DDS interoperability demonstration used scenarios such as:

* Basic connectivity to network using Internet Protocol (IP)
* Discovery of publishers and subscribers
* Quality of service (QoS) Compatibility between requester and offerer
* Delay-tolerant networking
* Multiple topics and instances of topics
* Exclusive ownerships of topics
* Content filtering of topic data including time and geographic

In 2004, the Object Management Group (OMG) published DDS version 1.0.

**[Object Management Group (OMG)](https://www.omg.org/)**<br>
Founded in 1989 by eleven companies (including Hewlett-Packard, IBM, Sun Microsystems, Apple Computer, American Airlines, iGrafx, and Data General), OMG's initial focus was to create a heterogeneous distributed object standard

![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c2/Notional_OMG_DDS_Interoperability.jpg/530px-Notional_OMG_DDS_Interoperability.jpg)
OMG Data Distribution Service interoperability

**Popular DDS vendors include:**<br>
* RTI
* ADLINK Technologies
* Twin Oaks Software

---
## ROS Installation
* [Installing ROS 2 on Ubuntu Linux](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Binary.html)
* [Installing ROS 2 on macOS](https://docs.ros.org/en/foxy/Installation/macOS-Install-Binary.html)
* [Installing ROS 2 o Windows](https://docs.ros.org/en/foxy/Installation/Windows-Install-Binary.html)

### Windows10 
*run WSL to install Ubuntu 20.04*<br>

**For Disk C:**
* Open **PowerShell** as administrator (管理者權限)<br>
`wsl --install -d ubuntu`<br>

**For Disk D:**
* Open **PowerShell** as administrator (管理者權限)<br>
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
```
Set-Location D:
New-Item WSL -ItemType Directory
Set-Location .\WSL
```
```
Invoke-WebRequest -Uri https://aka.ms/wslubuntu2004 -OutFile Ubuntu.appx -UseBasicParsing
```
```
Rename-Item .\Ubuntu.appx Ubuntu.zip
Expand-Archive .\Ubuntu.zip -Verbose
```

* Click **ubuntu2004.exe** to run installation<br>
```
installing, this may take a few minutes...
Enter new UNIX username: yourname 
Enter new UNIX password: ****
Retype new UNIX password: ****
passwd: password updated successfully
Installation successful!
```

---
### Ubuntu 20.04
**[Building ROS 2 on Ubuntu Linux](https://docs.ros.org/en/foxy/Installation/Ubuntu-Development-Setup.html)**<br>
`sudo apt update && sudo apt install curl gnupg2 lsb-release`<br>
`sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key  -o /usr/share/keyrings/ros-archive-keyring.gpg`<br>

* Add the repository to your sources list:
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(source /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

* Install development tools and ROS tools:
```
sudo apt update && sudo apt install -y \
  build-essential \
  cmake \
  git \
  libbullet-dev \
  python3-colcon-common-extensions \
  python3-flake8 \
  python3-pip \
  python3-pytest-cov \
  python3-rosdep \
  python3-setuptools \
  python3-vcstool \
  wget
# install some pip packages needed for testing
python3 -m pip install -U \
  argcomplete \
  flake8-blind-except \
  flake8-builtins \
  flake8-class-newline \
  flake8-comprehensions \
  flake8-deprecated \
  flake8-docstrings \
  flake8-import-order \
  flake8-quotes \
  pytest-repeat \
  pytest-rerunfailures \
  pytest
# install Fast-RTPS dependencies
sudo apt install --no-install-recommends -y \
  libasio-dev \
  libtinyxml2-dev
# install Cyclone DDS dependencies
sudo apt install --no-install-recommends -y \
  libcunit1-dev
```

* Get ROS2 Code:
```
mkdir -p ~/ros2_foxy/src
cd ~/ros2_foxy
wget https://raw.githubusercontent.com/ros2/ros2/foxy/ros2.repos
vcs import src < ros2.repos
```

* Install dependencies using rosdep
```
sudo rosdep init
rosdep update
rosdep install --from-paths src --ignore-src -y --skip-keys "fastcdr rti-connext-dds-5.3.1 urdfdom_headers"
```

* Packages for build failures
```
conda install curl
pip install catkin_pkg empy lark
sudo apt remove shiboken2 libshiboken2-dev libshiboken2-py3-5.14
pip install shiboken2
```

* Build the code in the workspace
```
cd ~/ros2_foxy
colcon build --symlink-install
```

* Environment setup
```
. ~/ros2_foxy/install/local_setup.bash
```

* Demo - Talker & Listener
![](https://github.com/rkuo2000/Robotics/blob/gh-pages/images/ROS2_demo_nodes_cpp-talker.png?raw=true)
![](https://github.com/rkuo2000/Robotics/blob/gh-pages/images/ROS2_demo_nodes_cpp-listener.png?raw=true)

* Uninstall
```
rm -rf ~/ros2_foxy
```

---
## [Gym-Gazebo](https://github.com/erlerobot/gym-gazebo)
an extension of the initial OpenAI gym for robotics using ROS and Gazebo<br>

GazeboCircuit2TurtlebotLidar-v0

![](https://github.com/erlerobot/gym-gazebo/blob/master/imgs/GazeboCircuit2TurtlebotLidar-v0.png?raw=true)

GazeboCircuitTurtlebotLidar-v0

![](https://github.com/erlerobot/gym-gazebo/blob/master/imgs/GazeboCircuitTurtlebotLidar-v0.png?raw=true)

GazeboCartPole-v0

![](https://github.com/erlerobot/gym-gazebo/blob/master/imgs/cartpole.jpg?raw=true)

GazeboModularArticulatedArm4DOF-v1

![](https://github.com/erlerobot/gym-gazebo/blob/master/imgs/GazeboModularArticulatedArm4DOF-v1.jpg?raw=true)

GazeboModularScara4DOF-v3

![](https://github.com/erlerobot/gym-gazebo/blob/master/imgs/GazeboModularScara4DOF-v3.png?raw=true)

GazeboModularScara3DOF-v3

![](https://github.com/erlerobot/gym-gazebo/blob/master/imgs/GazeboModularScara3DOF-v3.png?raw=true)

GazeboModularScara3DOF-v2

![](https://github.com/erlerobot/gym-gazebo/blob/master/imgs/GazeboModularScara3DOF-v2.png?raw=true)

ARIACPick-v0

![](https://github.com/erlerobot/gym-gazebo/blob/master/imgs/ariac_pick.jpg?raw=true)

---
### RDS
**[ROS Developement Studio](https://www.theconstructsim.com/)**<br>
![](https://www.theconstructsim.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-10-at-17.08.49-1024x486.png)

**[exploring-ros-2-wheeled-robot-part-01](https://www.theconstructsim.com/exploring-ros-2-wheeled-robot-part-01/)**<br>
![](https://www.theconstructsim.com/wp-content/uploads/2019/04/m2wr_gazebo.png)

---
## Micro-ROS
<img width="50%" height="50%" src="https://micro.ros.org/img/micro-ROS_big_logo.png">
micro-ROS puts ROS2 nodes onto microcontrollers

**[micro-ROS setup](https://github.com/micro-ROS/micro_ros_setup)**<br>
* [micro-ROS for Renesas e2 studio](https://github.com/micro-ROS/micro_ros_renesas2estudio_component)
* [micro-ROS component for ESP-IDF](https://github.com/micro-ROS/micro_ros_espidf_component)
* [micro-ROS module for Zephyr](https://github.com/micro-ROS/micro_ros_zephyr_module)
* [micro-ROS module for Mbed RTOS](https://github.com/micro-ROS/micro_ros_mbed)
* [micro-ROS app for Nuttx RTOS](https://github.com/micro-ROS/micro_ros_nuttx_app)
* [micro-ROS app for Microsoft Azure RTOS](https://github.com/micro-ROS/micro_ros_azure_rtos_app)
* [micro-ROS for STM32CubeMX/IDE](https://github.com/micro-ROS/micro_ros_stm32cubemx_utils)
* [micro-ROS for Arduino](https://github.com/micro-ROS/micro_ros_arduino)
* [micro-ROS module for Raspberry Pi Pico SDK](https://github.com/micro-ROS/micro_ros_raspberrypi_pico_sdk)

**ROS2 supported distributions are:**<br>
<style>table, th, td { padding: 10px; border: 1px solid black; border-collapse: collapse; }</style>
<table>
<tr><th>ROS 2 Distro</th><th>State</th><th>Branch</th></tr>
<tr><td>Crystal</td><td>EOL</td><td>`crystal`</td></tr>
<tr><td>Dashing</td><td>EOL</td><td>`dashing`</td></tr>
<tr><td>Foxy</td><td>Supported</td><td>`foxy`</td></tr>
<tr><td>Galactic</td><td>Supported</td><td>`galactic`</td></tr>
<tr><td>Rolling</td><td>Supported</td><td>`main`</td></tr>
</table>

### micro-ROS for Arduino
Download .zip and included by Arduion library manager

---
### ROS2 on ESP32
**Code:** [shirokunet/ros2_esp32bot](https://github.com/shirokunet/ros2_esp32bot)<br>
![](https://camo.githubusercontent.com/c7ee71399d568f5c97d8ca756219ebb68d3e103bd13128aa796e0dc221d80b6b/68747470733a2f2f6c68332e676f6f676c6575736572636f6e74656e742e636f6d2f7835734b45765f525168476d357143432d7a44466d46394d662d374b35577a506a704753575675765063647052715a4d4b6852634b344a5347366e36763844505434686c79576a6d4261437057565847535773667254553750326f7975305839576e65766e4667516c6c5579616547776857457846536451787243566f6c6e2d4a6f725a6944764d3041)

**Blog:** [如何使用esp32從零制作一個ROS2的teleop遙控器](https://chowdera.com/2021/10/20211023102532530v.html)<br>

![](https://inotgo.com/imagesLocal/202110/23/20211023102200379D_5.jpg)

**Blog:** [Setting up an ESP32 microcontroller for ROS2 robotics](https://blog.hadabot.com/set-up-esp32-microcontroller-for-ros2-robotics.html)<br>
![](https://blog.hadabot.com/images/hadabot_teleop__controller_01.jpg)

**Blog:** [micro-ROS porting to ESP32](https://discourse.ros.org/t/micro-ros-porting-to-esp32/16101)<br>
[core tutorials](https://micro.ros.org//docs/tutorials/core/overview/)<br>

```
ros2 run micro_ros_setup create_firmware_ws.sh freertos esp32

ros2 run micro_ros_setup configure_firmware.sh int32_publisher -t udp -i [your local machine IP] -p 8888

ros2 run micro_ros_setup build_firmware.sh menuconfig

# Now go to the micro-ROS Transport Settings → WiFi Configuration menu and fill your WiFi SSID and password. Save your changes, exit the interactive menu, and run:

ros2 run micro_ros_setup build_firmware.sh

# Connect your ESP32 to the computer with a micro-USB cable, and run:

ros2 run micro_ros_setup flash_firmware.sh
```

<br />
<br />

*This site was last updated {{ site.time | date: "%B %d, %Y" }}.*
