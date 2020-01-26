# EUFS Autonomous Simulation

## This entire package may include slight changes from the forked repo specific to my use case.
To use this repo clone this repo on master branch with the following repos also included in the workspace. 

It is designed to work with the melodic distro of ROS - not the kinetic one, so be sure to checkout the melodic branches of any repo you clone - if they exist. 

* robot_state_publisher https://github.com/JmcRobbie/robot_state_publisher
* image_pipeline https://github.com/JmcRobbie/image_pipeline
* geometry2 https://github.com/JmcRobbie/geometry2
* kdl_parser https://github.com/JmcRobbie/kdl_parser
* robotnik_msgs https://github.com/JmcRobbie/robotnik_msgs
* and any others that you decide to use/try.  


ROS/Gazebo simulation packages for driverless FSAE vehicles.

![simulation](https://eufs.eusa.ed.ac.uk/wp-content/uploads/2018/05/eufsa-sim.jpg)

### Contents
1. [Install Prerequisites](#requirements)
2. [Compiling and running](#compiling)
3. [Sensors](#sensors)

## Setup Instructions
### 1. Install Prerequisites <a name="requirements"></a>
##### - Install Ubuntu 18.04 LTS
##### - Install [ros-melodic-desktop-full](http://wiki.ros.org/melodic/Installation)
##### - Install ROS packages:
* ros-melodic-ackermann-msgs
* ros-melodic-twist-mux
* ros-melodic-joy
* ros-melodic-controller-manager
* ros-melodic-robotnik-msgs
* ros-melodic-velodyne-simulator
* ros-melodic-effort-controllers
* ros-melodic-velocity-controllers
* ros-melodic-joint-state-controller
* ros-melodic-gazebo-ros-control

Or if you are lazy like me here's a one-liner
```
sudo apt-get install ros-melodic-ackermann-msgs ros-melodic-twist-mux ros-melodic-joy ros-melodic-controller-manager ros-melodic-velodyne-simulator ros-melodic-effort-controllers ros-melodic-velocity-controllers ros-melodic-joint-state-controller ros-melodic-gazebo-ros-control
```

Then install additional ROS packages for controllers. Note that this command doesn't work well with `zsh`. 

```
sudo apt-get install ros*velocity*controller* ros*effort*controller* ros*position*controller*
```

After that, install the package for velodyne lidar sensor.

```
sudo apt install ros-melodic*velodyne*
```


### 2. Compiling and running <a name="compiling"></a>

Create a workspace for the simulation if you don't have one:
```
mkdir -p ~/ros/eufs_ws/src
```
Copy the contents of this repository to the `src` folder you just created.

```
cd ~/ros/eufs_ws/src
git clone https://github.com/JmcRobbie/eufs_sim
git clone https://github.com/JmcRobbie/robotnik_msgs
```


Navigate to your workspace and build the simulation:
```
cd ~/ros/eufs_ws
catkin_make
```
_Note:_ You can use `catkin build` instead of `catkin_make` if you know what you are doing. Please note that in order to use `catkin build` you would need to install the `catkin_tools` package. You can install this by doing:

```
sudo apt-get install python-catkin-tools
```

To enable ROS to find the EUFS packages you also need to run
```source /devel/setup.bash```
_Note:_ source needs to be run on each new terminal you open. You can also include it in your `.bashrc` file.

Now you can finally run our kickass simulation!!
```
roslaunch eufs_gazebo small_track.launch
```

An easy way to control the car is via
```
roslaunch robot_control rqt_robot_control.launch
```

### 3. Additional sensors <a name="sensors"></a>
Additional sensors for testing are avilable via the `ros-melodic-robotnik-sensor` package. Some of them are already defined in `eufs_description/robots/eufs.urdf.xarco`. You can simply commment them in and attach them appropriately to the car.


**Sensor suit of the car by default:**

* VLP16 lidar
* ZED Stereo camera
* IMU
* GPS
* odometry
