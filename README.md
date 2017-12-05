# Welcome to the Intel Aero ros-examples guide.

This doc guides how to build and run ros-examples.
##On native ROS

### PREREQUISITES

#### ROS
Install [ROS](http://wiki.ros.org/kinetic/Installation/Ubuntu) pacakges

#### MAVROS
Install [MAVROS](http://wiki.ros.org/mavros) packages

```
$ apt install ros-kinetic-mavros
```
### Clone and build ROS-examples
```
$ git clone https://github.intel.com/drones/ros-examples.git
$ catkin build
```
To add the workspace to your ROS environment you need to source the generated setup file:
```

$ . ~/ros-examples/devel/setup.bash
```
After `catkin_make` build is complete, ROS Node executable is generated in `devel/lib/mavros_offboard_ctrl/node` - this is the application by itself.

```
$ apt-get update
```
### Launching MAVROS
MAVROS automatically launches `roscore` which enables communication across ROS nodes.
```
$roslaunch mavros px4.launch fcu_url:="udp://:14540@<Aero-IP>:14557"
```

Goto **Aero terminal 1** and run the ROS Application node
```
# roslaunch aero_telemetry_simple aero_telemetry_simple.launch
```
This successfully launches launch file  which connects to Aero flight Controller via MAVROS.

## On docker ROS



