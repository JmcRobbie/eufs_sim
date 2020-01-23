# EUFS Autonomous Simulation

## This entire package may include slight changes from the forked repo specific to my use case.
To use this repo clone this repo on master branch with the following repos also included in the workspace. 

It is designed to work with the melodic distro of ROS - not the kinetic one, so be sure to checkout the melodic branches of any repo you clone - if they exist. 

* robot_state_publisher https://github.com/JmcRobbie/robot_state_publisher
* image_pipeline https://github.com/JmcRobbie/image_pipeline
* geometry2 https://github.com/JmcRobbie/geometry2
* kdl_parser https://github.com/JmcRobbie/kdl_parser
* robotnik_msgs https://github.com/JmcRobbie/robotnik_msgs
* + any others that you decide to use/try.  

Apparently this is important as well: 

sudo apt-get install ros*velocity*controller* ros*effort*controller* ros*position*controller*


Clone each of these repos into a workspace and build all with 

`catkin build`

ROS/Gazebo simulation packages for driverless FSAE vehicles.

![simulation](https://eufs.eusa.ed.ac.uk/wp-content/uploads/2018/05/eufsa-sim.jpg)

### Contents
1. [Install Prerequisites](#requirements)
2. [Compiling and running](#compiling)
3. [Sensors](#sensors)

## Setup Instructions
### 1. Install Prerequisites <a name="requirements"></a>
##### - Install Ubuntu 16.04 LTS
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

Or if you are lazy like my here's a one-liner
```
sudo apt-get install ros-melodic-ackermann-msgs ros-melodic-twist-mux ros-melodic-joy ros-melodic-controller-manager ros-melodic-robotnik-msgs ros-melodic-velodyne-simulator ros-melodic-effort-controllers ros-melodic-velocity-controllers ros-melodic-joint-state-controller ros-melodic-gazebo-ros-control ros-melodic-robotnik-msgs
```


### 2. Compiling and running <a name="compiling"></a>

Create a workspace for the simulation if you don't have one:
```mkdir -p ~/ros/eufs_ws/src```
Copy the contents of this repository to the `src` folder you just created.

Navigate to your workspace and build the simulation:
```
cd ~/ros/eufs_ws
catkin_make
```
_Note:_ You can use `catkin build` instead of `catkin_make` if you know what you are doing.

To enable ROS to find the EUFS packages you also need to run
```source /devel/setup.bash```
_Note:_ source needs to be run on each new terminal you open. You can also include it in your `.bashrc` file.

Now you can finally run our kickass simulation!!
```roslaunch eufs_gazebo small_track.launch```

An easy way to control the car is via
```roslaunch robot_control rqt_robot_control.launch```

### 3. Additional sensors <a name="sensors"></a>
Additional sensors for testing are avilable via the `ros-melodic-robotnik-sensor` package. Some of them are already defined in `eufs_description/robots/eufs.urdf.xarco`. You can simply commment them in and attach them appropriately to the car.


**Sensor suit of the car by default:**

* VLP16 lidar
* ZED Stereo camera
* IMU
* GPS
* odometry
