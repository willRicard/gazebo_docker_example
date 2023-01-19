# Argos3 Docker Example

This is a minimal Docker example to run a graphical Gazebo simulation on any
platform.

## Build the Image
For the first build execute in the same folder as the Dockerfile: 
```
docker build -t inf3995-equipe0-simulation .
```

## Running a Container

The Gazebo simulation needs access to a graphical user interface to work.
Hence, this example uses [TurboVNC](https://turbovnc.org) on top of [VirtualGL](https://virtualgl.org) so you can connect to the
GUI and run apps using 3D graphics.

You can start a bash shell in the container with the following command: 
```
docker run -p 5901:5901 -it inf3995-equipe0-simulation bash
```

From there, you can launch the GUI and connect to `localhost:5901` using a VNC client
```
cd /root
source .profile
TVNC_WM=openbox-session vncserver # will prompt for a password
```

Then you can start the simulation yourself from the virtual desktop (default
window manager is OpenBox, right-click the desktop and select Terminal).

For example, go into the folder `/inf3995_ws`
and execute :
```
catkin_make && source devel/setup.bash
roslaunch limo_gazebo_sim limo_ackerman.launch &
python3 /opt/ros/noetic/lib/teleop_twist_keyboard/teleop_twist_keyboard.py # you can drive around
```
