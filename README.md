# Demo mapping my room
[![Watch the video](https://img.youtube.com/vi/fRMxI-7EaYo/sddefault.jpg)](https://youtu.be/fRMxI-7EaYo)
# snitch_launch_pkg
This repository contains all the launch files for the platform:
```
git clone https://github.com/SnitchTr/snitch_launch_pkg
```
# How to use the snitch
First you'll need to open 3 terminals:
On terminal 1 you'll want to launch the platform itself
```
bash launch_camera.sh
```
On terminal 2 you'll want to launch the human detection (note: this is not a strictly required test for the platform to "work" but without it it won't perform any human detection)
```
bash human_detector_launch.sh
```
On terminal 3 you'll want to run the keyboard tool to use the temporary manual control system:
```
cd catkin_ws/
catkin_make
source devel/setup.sh
rosrun test_pkg keyboard.py
```
To use the keyboard as a remote controller you'll want to set the data type as a UInt8, and the topic as dir. Note: you can make this settings permanent dor the sesion by writing keep when chosing topic or data type.
The direction commands are:
stop = 0
foward = 1
backward = 2
left = 3
right = 4
anything else will be interpreted as a 0 and stop the platform.
# Using the snitch with multiple computers
If you have multiple computers with ros installed you can use the keyboard on the computer that isn't on the snitch to make driving easier.
On the computer 1, the one on the snitch you'll want to set up the rosmaster to allow an external connection.
To do that you'll want to open up a terminal and set the ROS_IP to the IP adress of the computer. To get the IP adress you can run the followning command:
```
Hostname -I
```
To set up the ROS_IP you can use the following command where [computer 1 IP adress] is the IP adress you got from the previous comand:
```
export ROS_IP= [computer 1 IP adress]
```
Then set up terminal 1 and 2 from the previous section making sure you set the correct ROS_IP on the terminal before strating the diferent nodes.
Terminal 1:
```
bash launch_camera.sh
```
Terminal 2:
```
bash human_detector_launch.sh
```
Note: you can do that with ssh too if you have it set up it is more convinient.

On the second computer you'll want to connect to the first computer by setting the ROS_IP and ROS_MASTER_URI correctly.
You can set the ROS_IP like you did on the same computer making sure you set it to the IP adress of the second computer:
```
export ROS_IP= [computer 2 IP adress]
```
To set the ROS_MASTER_URI you'll want to run the following comand
```
ROS_MASTER_URI=http://[computer 1 IP adress]:11311
```
To connect to computer 1 you'll want to make sure the ROS_MASTER_URI are the same so on the URI you have to write computer's 1 IP adress.
Once you are connected you can run the keyboard.py node to control the platform remotely.
```
cd catkin_ws/
catkin_make
source devel/setup.sh
rosrun test_pkg keyboard.py
```
