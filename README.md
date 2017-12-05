# Welcome to the Intel Aero ros-examples guide.

This doc guides how to build and run ros-examples.
## Building and running ROS Application on  Intel Aero platform
### Clone and build
```
$ git clone https://github.intel.com/drones/ros-examples.git
$ catkin_make
```
To add the workspace to your ROS environment you need to source the generated setup file:
```

$ . ~/ros-examples/devel/setup.bash
```
After `catkin_make` build is complete, ROS Node executable is generated in `devel/lib/mavros_offboard_ctrl/node` - this is the application by itself.

### Pull ROS docker in Aero platorm
Open a **Aero terminal 1** and pull ros packages using docker.
```
# docker pull ros
```

### Run ROS in docker container
```
# docker run -it --privileged ros
```
this opens a ROS shell with container-id

### Update packages
```
root@1bb62dbedaf0:/# apt-get update
```

### Install [MAVROS](http://wiki.ros.org/mavros) packages
```
root@1bb62dbedaf0:/# apt install ros-kinetic-mavros
```

Save your work by committing this container using [docker commit](https://docs.docker.com/engine/reference/commandline/commit/). Open another **Aero terminal 2**.
```
# docker commit -m "Demo of ROS App" 1bb62dbedaf0 my_container/ros
```

### Launching MAVROS
MAVROS automatically launches `roscore` which enables communication across ROS nodes.
```
roslaunch mavros px4.launch fcu_url:="udp://:14540@<Aero-IP>:14557"
```

Goto **Aero terminal 1** and run the ROS Application node
```
# rosrun aero_telemetry_simple node
```
This successfully launches ROS Application node (used `aero_telemetry_simple` as example) which connects to Aero Flight Controller via MAVROS. 

OR
```
# roslaunch aero_telemetry_simple aero_telemetry_simple.launch
```
This successfully launches launch file  which connects to Aero flight Controller via MAVROS.



## Offboard Control:
* Listens for State of the Aero Flight Controller
* Provides offboard setpoint's.
* Sets OFFBOARD mode.
* When Aero Flight Controller changes to OFFBOARD mode, it detects slow takeoff with altitude of 2 meters.
* State callabck gets called indicating Aero FC state change.

## Fly mission:
* Loads the QGC mission plan (passed in command-line)
* Composes waypoints & sends them to the vehicle
* Sets Vehicle to MISSION mode. This causes Vehicle to executes the mission.
* Shuts down after the mission is accomplished

**Before you run** `mavros_fly_mission`:
* Plan your missions in [QGC](http://qgroundcontrol.com) & save them to a file.

Note: `aero_fly_mission` supports only QGC mission plan now. 

## Simple Takeoff Land
* Waits for  Flight Controller connection.
* Takeoff with minimum altitude of 2.5m.
* Wait for 5 seconds.
* Land to current position.
 

## Telemetry simple
* Waits for Flight Controller connection
* Gives telemetry information such as global position, relative altitude, local position, battery status and velocity.

## Telemetry modes
* Waits for Flight Controller connection.
* Displays mode of the Flight

## Offboard Velocity
* Waits for Flight Controller connection.
* Takeoff with minimun altitude of 2.5m.
* Move the drone with local NED offboard velocity with different parameters.
* Land at the current position.
* Again takeoff with minimum altitude of 2.5m
* Move drone with local Body offboard velocity with different parameters.
