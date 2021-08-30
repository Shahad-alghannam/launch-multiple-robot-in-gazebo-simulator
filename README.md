# launch-multiple-robot-in-gazebo-simulator

Install ROS 1 on Remote PC

$ sudo apt-get update
$ sudo apt-get upgrade
$ wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_kinetic.sh
$ chmod 755 ./install_ros_kinetic.sh
$ bash ./install_ros_kinetic.sh

Install Dependent ROS 1 Packages

$ sudo apt-get install ros-kinetic-joy ros-kinetic-teleop-twist-joy 
ros-kinetic-teleop-twist-keyboard ros-kinetic-laser-proc 
ros-kinetic-rgbd-launch ros-kinetic-depthimage-to-laserscan 
ros-kinetic-rosserial-arduino ros-kinetic-rosserial-python 
ros-kinetic-rosserial-server ros-kinetic-rosserial-client 
ros-kinetic-rosserial-msgs ros-kinetic-amcl ros-kinetic-map-server 
ros-kinetic-move-base ros-kinetic-urdf ros-kinetic-xacro 
ros-kinetic-compressed-image-transport ros-kinetic-rqt* 
ros-kinetic-gmapping ros-kinetic-navigation ros-kinetic-interactive-markers

Install TurtleBot3 Packages

$ sudo apt-get install ros-kinetic-dynamixel-sdk
$ sudo apt-get install ros-kinetic-turtlebot3-msgs
$ sudo apt-get install ros-kinetic-turtlebot3

expand more details about building TurtleBot3 package from source.

$ sudo apt-get remove ros-kinetic-dynamixel-sdk
$ sudo apt-get remove ros-kinetic-turtlebot3-msgs
$ sudo apt-get remove ros-kinetic-turtlebot3
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/src/
$ git clone -b kinetic-devel https://github.com/ROBOTIS-GIT/DynamixelSDK.git
$ git clone -b kinetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
$ git clone -b kinetic-devel https://github.com/ROBOTIS-GIT/turtlebot3.git

$ echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc

Set TurtleBot3 Model Name

• TurtleBot3 Burger

$ echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc

• TurtleBot3 Waffle Pi

$ echo "export TURTLEBOT3_MODEL=waffle_pi" >> ~/.bashrc

OpenCR Setup

$ sudo dpkg --add-architecture armhf
$ sudo apt-get update
$ sudo apt-get install libc6:armhf

$ export OPENCR_PORT=/dev/ttyACM0
$ export OPENCR_MODEL=burger
$ rm -rf ./opencr_update.tar.bz2

$ wget https://github.com/ROBOTIS-GIT/OpenCR-Binaries/raw/master/turtlebot3/ROS1/latest/opencr_update.tar.bz2
$ tar -xvf opencr_update.tar.bz2

$ cd ./opencr_update
$ ./update.sh $OPENCR_PORT $OPENCR_MODEL.opencr

Run SLAM Node

$ roscore

$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_slam turtlebot3_slam.launch

• defining TurtlBot3 Waffle Pi as a default model.

$ echo 'export TURTLEBOT3_MODEL=waffle_pi' >> ~/.bashrc
$ source ~/.bashrc

• Gmapping

$ roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping

• Run Teleoperation Node

$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

Gazebo Simulation

Install Simulation Package

$ cd ~/catkin_ws/src/
$ git clone -b kinetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
$ cd ~/catkin_ws && catkin_make

(TurtleBot3 World)

$ export TURTLEBOT3_MODEL=waffle
$ roslaunch turtlebot3_gazebo turtlebot3_world.launch

Operate TurtleBot3

$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

run Autonomous Collision Avoidance
$ roslaunch turtlebot3_gazebo turtlebot3_simulation.launch

visualize Simulation data(RViz)
$ roslaunch turtlebot3_gazebo turtlebot3_simulation.launch

SLAM Simulation

• Launch Simulation World
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_gazebo turtlebot3_world.launch

• Run SLAM Node
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping

• Run Teleoperation Node
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

• Save Map
$ rosrun map_server map_saver -f ~/maphttps://user-images.githubusercontent.com/81427704/125122685-72f66f00-e0fe-11eb-8c33-6fd8eb259080.MOVhttps://user-images.githubusercontent.com/81427704/125122744-80135e00-e0fe-11eb-9075-02c27b347dd8.MOV
