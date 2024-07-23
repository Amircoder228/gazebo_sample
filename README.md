# Dependency installation for running a Gazebo MAVROS simulation

To run the simulation, the following dependencies need to be installed:
* Pixhawk
* ros
* mavros
* gazebo
## Install PX4
1. Download PX4 Source Code

        git clone https://github.com/PX4/PX4-Autopilot.git --recursive
2. Run the ubuntu.sh the --no-sim-tools (and optionally --no-nuttx):

        bash ./PX4-Autopilot/Tools/setup/ubuntu.sh --no-sim-tools --no-nuttx
3. Restart the computer on completion.
## Install ros noetic
1. Setup your sources.list

        sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
2. Set up your keys

        sudo apt install curl # if you haven't already installed curl
        curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
3. Installation
    
    First, make sure your Debian package index is up-to-date: 

         sudo apt update

    Desktop-Full Install: (Recommended) : Everything in Desktop plus 2D/3D simulators and 2D/3D perception packages 

        sudo apt install ros-noetic-desktop-full
4. Environment setup

    It can be convenient to automatically source this script every time a new shell is launched. These commands will do that for you. 

        echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
        source ~/.bashrc

5. Dependencies for building packages

    To install this tool and other dependencies for building ROS packages, run: 

        sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential

        sudo apt install python3-rosdep

        sudo rosdep init
        rosdep update7     
## Binary Installation Mavros

    sudo apt-get install ros-${ROS_DISTRO}-mavros ros-${ROS_DISTRO}-mavros-extras ros-${ROS_DISTRO}-mavros-msgs

Then install GeographicLib datasets.

        wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh
        sudo bash ./install_geographiclib_datasets.sh

## Install Gazebo

1. Setup your computer to accept software from packages.osrfoundation.org.

        sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'

    You can check to see if the file was written correctly. For example, in Ubuntu Xenial, you can type:

        $ cat /etc/apt/sources.list.d/gazebo-stable.list
        deb http://packages.osrfoundation.org/gazebo/ubuntu-stable xenial main

1. Setup keys

        wget https://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -

1. Install Gazebo.

    First update the debian database:

        sudo apt-get update

    Next install gazebo-11 by:

        sudo apt-get install gazebo11

1. Check your installation

    ***Note*** The first time `gazebo` is executed requires the download of some models and it could take some time, please be patient.

        gazebo

## Other dependency need to be installed:

        sudo apt-get install protobuf-compiler libeigen3-dev libopencv-dev -y libgstreamer-plugins-base1.0-dev gstreamer1.0-plugins-bad gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-ugly -y

## Run Simulation
1. clone repository.

        git clone https://github.com/Amircoder228/gazebo_sample.git

2. Launch `mavros` with the specified FCU URL.

        roslaunch mavros px4.launch fcu_url:=udp://:14540@127.0.0.1:14557

3. in second terminal Run the `PX4` simulation.

        make px4_sitl_default gazebo
        
4. cd to workspase.

        cd gazebo_sample
5. Build workspace and source the setup file.

        catkin_make
        source devel/setup.bash
6. in therd terminal Run custom ROS node such as `offb_node`.

        rosrun offb_node offb_node_node 
