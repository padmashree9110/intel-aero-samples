# Welcome to the Intel Aero ros-examples guide.

This doc guides how to build and run ros-examples.
## On native ROS

### Prerequisites

#### ROS
Install [ROS](http://wiki.ros.org/kinetic/Installation/Ubuntu) pacakges

#### MAVROS
Install [MAVROS](http://wiki.ros.org/mavros) packages
```
$ apt install ros-kinetic-mavros ros-kinetic-mavros-extras

```
Then install GeographicLib datasets by running the install_geographiclib_datasets.sh script:
```
$ wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh
$ ./install_geographiclib_datasets.sh
```

### Catkin
Install catkin packages
```
$sudo apt-get update
$sudo apt-get install python-catkin-tools
```

### Clone and build ROS-examples
```
$ git clone https://github.intel.com/drones/ros-examples.git
$ cd ros-examples
$ catkin build
```
To add the workspace to your ROS environment you need to source the generated setup file:
```
$ source devel/setup.bash
```

### Update Packages
```
$ apt-get update
```

### Launching MAVROS
MAVROS automatically launches `roscore` which enables communication across ROS nodes.
```
$roslaunch mavros px4.launch fcu_url:="udp://:14540@<Aero-IP>:14557"
```

Open another terminal  and run the ROS launch file
```
# roslaunch aero_telemetry_simple aero_telemetry_simple.launch
```
This successfully launches launch file  which connects to Aero flight Controller via MAVROS.

## On docker ROS

### Prerequisites

Open two terminals (docker1 and docker2) and do below steps in both.

#### ROS
Pull ros packages using docker
```
$ docker pull ros
```
Run ROS in docker container
```
$ docker run -it --privileged ros
```
this opens a ROS shell with container-id

#### MAVROS
Install [MAVROS](http://wiki.ros.org/mavros) packages
```
# apt install ros-kinetic-mavros ros-kinetic-mavros-extras
```

Then install GeographicLib datasets by running the install_geographiclib_datasets.sh script:
```
$ wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh
$ ./install_geographiclib_datasets.sh
```

### Catkin
Install catkin packages
```
#sudo apt-get update
#sudo apt-get install python-catkin-tools
```

### Update Packages
```
# apt-get update
```

## Launching MAVROS(In docker1)

### Export proxy settings
```
export ROS_IP=<IP of docker1>
export ROS_MASTER_URI="http://<IP of docker1>:11311"
```

### Launch mavros
```
#roslaunch mavros px4.launch fcu_url:="udp://:14540@<Aero-IP>:14557"
```

## Running ROS-examples(In Docker2)

### Clone and build ROS-examples
```
$ git clone https://github.intel.com/drones/ros-examples.git
$ cd ros-examples
$ catkin build
```

To add the workspace to your ROS environment you need to source the generated setup file:
```
$ source devel/setup.bash
```

### Export proxy settings
```
export ROS_IP=<IP of docker1>
export ROS_MASTER_URI="http://<IP of docker1>:11311"
```

### Run ROS application using
```
# roslaunch aero_telemetry_simple aero_telemetry_simple.launch
```

# EXAMPLE : Fly mission

* Loads the QGC mission plan (passed in command-line)
* Composes waypoints & sends them to the vehicle
* Sets Vehicle to MISSION mode. This causes Vehicle to executes the mission.

**Before you run** `mavros_fly_mission`:
* Plan your missions in [QGC](http://qgroundcontrol.com) & save them to a file.
Note: `mavros_fly_mission` supports only QGC mission plan now.

Running fly_mission examples
```
$roslaunch aero_fly_mission aero_fly_mission.launch file
Note: Give absolute path to the file
```



