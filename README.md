# Homework2-RL2024
#  Overview
The goal of this homework is to dynamically control a 7-DoF robot manipulator using Docker and ROS2 with RViz and Gazebo, ensuring it follows a desired trajectory in both joint space and operational space. The repository contains instructions to download the folders from GitHub, launch the robot, and run the controller.
# Setup  
Open the terminal, launch the container, and navigate to the directory where you want to download the folder. Then, clone the repository with:
```
git clone https://github.com/paola-P-99/Homework2-RL2024.git
```

To build the packages, navigate to the ROS2 workspace and build them with:
```
colcon build
```

Afterward, source the workspace:
```
source install/setup.bash
```

# Launching the robot 
The robot can be controlled using 3 command interfaces:
    • Position 
    • Velocity 
    • Effort 
If you want to apply a position controller, you need to launch the file with the position interface, which is the default one. To do this, run the following command:
```
ros2 launch iiwa_bringup iiwa.launch.py 
```

If you want to apply a velocity controller, you need to launch the file with the velocity interface. To do this, run the following command:
```
ros2 launch iiwa_bringup iiwa.launch.py  command_interface:="velocity" robot_controller:="velocity_controller"
```

If you want to apply an effort controller, you need to launch the file with the effort interface. To do this, run the following command:
```
ros2 launch iiwa_bringup iiwa.launch.py command_interface:="effort" robot_controller:="effort_controller" use_sim:=true
```

# Running the controllers 
To run the node with the controller, open another terminal, connect to the same Docker container, and execute the following command.
To ensure the proper visualization of the control action, the controllers activated must match the selected interface; otherwise, you won’t be able to see the robot moving.

If you selected a position interface, run the following command:
```
ros2 run ros2_kdl_package ros2_kdl_node
```

If you selected a velocity interface, run the following command:
```
ros2 run ros2_kdl_package ros2_kdl_node --ros-args -p cmd_interface:=velocity
```

If you selected an effort interface, run the following command:
```
ros2 run ros2_kdl_package ros2_kdl_node --ros-args -p cmd_interface:=effort
```

# Choosing the control action
The code provides the option to choose between a circular or rectilinear trajectory, with both trapezoidal or polynomial velocity profiles. To do this, you need to:
`press a number between 1 and 4 then enter  `
The controllers provided are two: one in joint space, implemented as a PD+ controller, and one in operational space, implemented as an Inverse Dynamics controller. To select between the two, you need to:
`press 1 or 2 then enter`
