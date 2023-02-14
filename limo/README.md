# Limo Docker Example

This is a minimal Docker example to deploy your project on the AgileX Limo robot.

## Build the image

For the first build execute in the same folder as the Dockerfile:

```
docker build -t inf3995-equipe0-limo .
```

## Running a container

The Limo deployment container needs to access serial devices (eg. `/dev/ttyTHS1`) to work.

You can start a bash shell in the container with the following command:

```
docker run --privileged --network=host -it inf3995-equipe0-limo bash
```

From there, you can use `ROS_MASTER_URI` to control the Limo from inside the container.

For example, go into the folder `/agx_ws` and execute:

```
catkin_make && source devel/setup.bash
roslaunch limo_bringup limo_start.launch
```

and on the remote machine or the Limo:

```
python3 /opt/ros/noetic/lib/teleop_twist_keyboard/teleop_twist_keyboard.py # you can drive around
```
