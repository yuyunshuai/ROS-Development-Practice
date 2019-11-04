# ROS Development Practice
This manual is for the courses oganized by AI_ROBOT@STSP.  
If you are interested in this document and looking for a lecturer, please contact me.  
My email address is: yys@nfu.edu.tw

## Install ROS

### 1. Install ROS on Ubuntu (PC)
Install ROS on the Remote PC.  

	sudo apt-get update
    sudo apt-get upgrade
    wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_kinetic.sh && chmod 755 ./install_ros_kinetic.sh && bash ./install_ros_kinetic.sh
    sudo reboot

Install dependent packages.

    sudo apt-get install ros-kinetic-joy ros-kinetic-teleop-twist-joy ros-kinetic-teleop-twist-keyboard ros-kinetic-laser-proc ros-kinetic-rgbd-launch ros-kinetic-depthimage-to-laserscan ros-kinetic-rosserial-arduino ros-kinetic-rosserial-python ros-kinetic-rosserial-server ros-kinetic-rosserial-client ros-kinetic-rosserial-msgs ros-kinetic-amcl ros-kinetic-map-server ros-kinetic-move-base ros-kinetic-urdf ros-kinetic-xacro ros-kinetic-compressed-image-transport ros-kinetic-rqt-image-view ros-kinetic-gmapping ros-kinetic-navigation ros-kinetic-interactive-markers

Install dependent packages for TurtleBot3.

    cd ~/catkin_ws/src/
    git clone https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
    git clone https://github.com/ROBOTIS-GIT/turtlebot3.git
    cd ~/catkin_ws && catkin_make

If the following error happens,

    The program 'catkin_make' is currently not installed. 
    You can install it by typing: sudo apt install catkin

run the below command and then catkin_make again.

    source /opt/ros/kinetic/setup.bash

Network configuration

    export ROS_MASTER_URI=http://IP_OF_REMOTE_PC:11311
    export ROS_HOSTNAME=IP_OF_REMOTE_PC


### 2. Install ROS on Ubuntu (TurtleBot3)
Download [Ubuntu MATE 16.04](https://ubuntu-mate.org/raspberry-pi/ubuntu-mate-16.04.2-desktop-armhf-raspberry-pi.img.xz)

Write an Ubuntu MATE image to microSD

    sudo apt-get install gnome-disk-utility

Use [GNOME Disks](https://www.youtube.com/watch?v=V_6GNyL6Dac) to write the image.  

Install ROS on the Raspberry Pi 3.  

	sudo apt-get update
    sudo apt-get upgrade
    wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_kinetic_rp3.sh && chmod 755 ./install_ros_kinetic_rp3.sh && bash ./install_ros_kinetic_rp3.sh
    sudo reboot

Install Dependent ROS Packages
    
    cd ~/catkin_ws/src
    git clone https://github.com/ROBOTIS-GIT/hls_lfcd_lds_driver.git
    git clone https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
    git clone https://github.com/ROBOTIS-GIT/turtlebot3.git
    cd ~/catkin_ws/src/turtlebot3
    sudo rm -r turtlebot3_description/ turtlebot3_teleop/ turtlebot3_navigation/ turtlebot3_slam/ turtlebot3_example/
    sudo apt-get install ros-kinetic-rosserial-python ros-kinetic-tf
    sudo reboot
    source /opt/ros/kinetic/setup.bash
    cd ~/catkin_ws && catkin_make -j1

Use USB port for OpenCR without acquiring root permission.

    rosrun turtlebot3_bringup create_udev_rules

Network configuration

    export ROS_MASTER_URI=http://IP_OF_REMOTE_PC:11311
    export ROS_HOSTNAME=IP_OF_TURTLEBOT

### 3. OpenCR setup
On turtlebot3 burger

    export OPENCR_PORT=/dev/ttyACM0
    export OPENCR_MODEL=burger
    rm -rf ./opencr_update.tar.bz2
    wget https://github.com/ROBOTIS-GIT/OpenCR-Binaries/raw/master/turtlebot3/ROS1/latest/opencr_update.tar.bz2 && tar -xvf opencr_update.tar.bz2 && cd ./opencr_update && ./update.sh $OPENCR_PORT $OPENCR_MODEL.opencr && cd ..
