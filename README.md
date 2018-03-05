# kinova-robotics-setup
A description on how to setup the kinova robotics ROS on a Ubuntu 14.04 system

## Install Ubuntu 14.04 
The images are available [here](http://releases.ubuntu.com/14.04/). Use the 64 Bit Version to avoide compatibility issues. This tutorial should also work with an existing setup but has only been tested on a fresh install.

## Install ROS Indigo 
The commands are [here](http://wiki.ros.org/indigo/Installation/Ubuntu)

Please note the following:
* In step 1.4 use `sudo apt-get install ros-indigo-desktop-full` to get most of the required packages
* Make sure you follow the steps until 1.7 and run the appropriate commands

## Install dependencies

We need some tools to run the installation process. Run the following commands:

* `sudo apt-get install git`

We also need some ROS dependencies:

```
sudo apt-get install ros-indigo-moveit ros-indigo-trac-ik ros-indigo-opencv3
```


## Setup Kinova

We will now setup the kinova ros environment.

First run this:
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
git clone https://github.com/Kinovarobotics/kinova-ros.git kinova-ros
cd ~/catkin_ws
catkin_make
```

Finally add the repo to your environment


```
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

## Run RVIZ
To finally run simulation of the robot use this:
```
roslaunch j2n6s300_moveit_config j2n6s300_virtual_robot_demo.launch
```
## Run with Real Robot
if a real robot is connected to the computer via USB, you can bring up the controll via the following steps. First a one time setup is required:
```
sudo cp ~/catkin_ws/src/kinova-ros/kinova_driver/udev/10-kinova-arm.rules /etc/udev/rules.d/
```
then each time you have to run two commands in seperate shells:
```
roslaunch kinova_bringup kinova_robot.launch kinova_robotType:=j2n6s300
```
and in the other shell
```
roslaunch j2n6s300_moveit_config j2n6s300_demo.launch
```

