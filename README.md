# ROS Differential Drive

This repo is for testing a simple Differential Drive Robot with ROS Kinetic Kame on Ubuntu 16. It is simulated with Gazebo, and visualized with RViz. The robot should be controlled by keyboard commands, or should perform endless circle or square oeprations. At first I tried doing it from scratch, but quickly found that I would run out of time, and then switched over to the TurtleBot, the most well-known open-source differential drive robot.

Instructions for: [1. Installation](https://github.com/jmcmahon443/differential_drive#1-installation), and [2. Operation](https://github.com/jmcmahon443/differential_drive#2-operation) are included.

## 1. Installation

These are the steps for installing Ubuntu 16, ROS Kinetic, and some TurtleBot dependencies.

### Install Ubuntu 16 on partition from USB stick

`https://help.ubuntu.com/community/Installation/FromUSBStick`

Find or buy a USB stick with at least 2GB of memory. Either format it to be bootable and install the Ubuntu 16 iso yourself or follow the links above. Then plug it into a PC and install Ubuntu 16 on an existing or new partition.

`https://www.ubuntu.com/download/desktop/create-a-usb-stick-on-macos`

I am using macOS to format the USB stick and install the iso, so I followed the above link, which uses the `unetbootin` application.

### Install ROS Kinetic Kame

`http://wiki.ros.org/kinetic/Installation/Ubuntu`

Copy the ROS Kinetic debian file.

```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116`
sudo apt-get update
```

At this point I updated Ubuntu 16 software, installed `git`, any hardware drivers, and Sublime Text 3. These steps are not included in this documentation, as they depend on preferred development workflow. For example, for my Nvidia 860M graphics card, I find it useful to use the packages below. After installing the drivers, go into System Settings to select the latest one and reboot.

```
sudo apt install nvidia-settings
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update
```

Install ROS Kinetic and TurtleBot packages.

```
sudo apt-get install ros-kinetic-desktop-full ros-kinetic-turtlebot-gazebo ros-kinetic-turtlebot-teleop
```

`rosdep update`

`echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc`

`source ~/.bashrc`

You do not need it for this ROS package, but it is helpful to install Python `rosinstall`

`sudo apt-get install python-rosinstall`

`http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment`

Check that the installation was successful. `printenv | grep ROS` should return:

```
ROS_ROOT=/opt/ros/kinetic/share/ros
ROS_PACKAGE_PATH=/opt/ros/kinetic/share
ROS_MASTER_URI=http://localhost:11311
ROSLISP_PACKAGE_DIRECTORIES=
ROS_DISTRO=kinetic
ROS_ETC_DIR=/opt/ros/kinetic/etc/ros
```

## 2. Operation

Set up a new catkin workspace, as per usual with any ROS package.

```
mkdir -p catkin_ws/src
cd catkin_ws/src
catkin_init_workspace
```

Then clone this repository, which is a collection of ROS packages, into the `src` folder: `git clone https://github.com/jmcmahon443/differential_drive.git`

All that is left is the compile the packages in the workspace, the `catkin_ws` folder.

```
cd ..
catkin_make
```

IMPORTANT: every time you open a new terminal window to execute within the workspace, you must source it to the workspace: `source devel/setup.bash`

### rviz, urdf

First, test the differential drive robot's urdf file with rviz `roslaunch differential_drive_description differential_drive_rviz.launch`

Now close the rviz window and `ctrl+c` in the terminal window to stop execution.

### gazebo

Next, test the differential drive robot's gazebo file `roslaunch differential_drive_gazebo differential_drive_world.launch`

Again close the gazebo window and `ctrl+c` in the terminal window to stop execution.

This robot is not properly designed, and it takes a very long time to do so. For this reason, skip ahead to opening the TurtleBot in gazebo. The TurtleBot is a robust differential drive system and is well supported by the open-source community.

```
roslaunch turtlebot_demo turtlebot_empty_world.launch
```

### teleop

The TurtleBot has some built keyboard teleop commands. Keep the previous gazebo screen open, start a new terminal window, source it, and run `roslaunch turtlebot_teleop keyboard_teleop.launch`

Unfortunately, I did not have time to get the teleop working via launch parameters, as specified. I also did not have time to implement a differential drive controller to perform the below circle and square operations.

![TurtleBot demo screenshot](https://raw.githubusercontent.com/jmcmahon443/differential_drive/master/turtlebot_demo.png)

### circle
`TODO.`

### square
`TODO.`
