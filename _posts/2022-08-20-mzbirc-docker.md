---
title:  "MZBIRC simulation with docker."
categories: mzbirc ignition gazebo docker dockwater
---

The [MBZIRC Maritime Grand Challenge simulator](https://github.com/osrf/mbzirc) includes instruction for running with docker, but lately our team has been using the [dockwater](https://github.com/Field-Robotics-Lab/dockwater) project workflow as a way to support many independent development environments, while making use of the [rocker](https://github.com/osrf/rocker) tool which supports interactive development concurrently in containers and using the host filesystem.

This is a how-to associated with running MBZIRC within a custom dockwater container.


## Build the mbzirc dockwater image

Clone the repo and switch to the branch for mbzirc
```
mkdir ~/WorkingCopies
cd ~/WorkingCopies
git clone git@github.com:Field-Robotics-Lab/dockwater.git
cd dockwater
git switch bsb/mbzirc
```

Build the mbzirc image
```
./build.bash mbzirc
```


## Host setup

Because the dockwater tool will use rocker to mount the host home directory, we can work with workspaces that are directly on the host.

Make the ROS 2 workspace and clone the repos.

```
cd
mkdir -p mbzirc_ws/src
cd mbzirc_ws/src
git clone git@github.com:osrf/mbzirc.git
git clone https://github.com/osrf/ros_ign.git -b galactic
git clone git@github.com:bsb808/mbzirc_demo.git
```

Note: Currently we need to build the [`ros_ign package`](https://index.ros.org/p/ros_ign/#galactic) from source - otherwise get a build error:  
```
--- stderr: mbzirc_seed                                                                    
In file included from /home/bsb/mbzirc_ws/src/mbzirc/mbzirc_seed/src/ReadRfRange.cpp:18:
/home/bsb/mbzirc_ws/src/mbzirc/mbzirc_seed/include/mbzirc_seed/ReadRfRange.hh:23:10: fatal error: ros_ign_interfaces/msg/param_vec.hpp: No such file or directory
   23 | #include <ros_ign_interfaces/msg/param_vec.hpp>
```

## Run a the container with rocker

Run the container using the included convenience script.

```
~/WorkingCopies/dockwater/run.bash dockwater:mbzirc
```

Then, in separate terminals, join a few so that you have bash shells running in the same container.

```
~/WorkingCopies/dockwater/join.bash dockwater_mbzirc_runtime
```

I use the [terminator](https://terminator-gtk3.readthedocs.io/en/latest/) tool to have five shell sessions within the container in a single window like this...
![image tooltip here](/assets/images/terminator.png)

## Build and run the mbzirc example

Within the container


```
source /opt/ros/galactic/setup.bash
cd ~/mbzirc_ws/
colcon build --symlink-install  
```

Run demo from https://github.com/osrf/mbzirc/wiki/Running-the-Demo

```
source ~/mbzirc_ws/install/setup.bash
ros2 launch mbzirc_ros competition_local.launch.py ign_args:="-v 4 -r simple_demo.sdf"
```


