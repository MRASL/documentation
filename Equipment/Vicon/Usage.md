# Using Vicon data

## Using ROS

For all of the following packages use the server IP defined in our [LAN setup page](/Equipment/Networking/LAN.html).

### ETHZ's Autonomous Systems Lab [VRPN Client](https://github.com/ethz-asl/ros_vrpn_client)

Same client used in [Dynamic System Identification, and Control for a cost effective open-source VTOL MAV](https://arxiv.org/pdf/1701.08623.pdf). Provides position, orientation, velocity and angular velocity. Connects to the Vicon server through the Virtual Reality Peripheral Network. Data seems to pass through a Luenberger state observer for position and linear velocity estimation and an Extended Kalman Filter for orientation and angular velocity estimation.

### ETHZ's Autonomous Systems Lab [Vicon Bridge](https://github.com/ethz-asl/vicon_bridge)

Use this if you want unfiltered data directly from the Vicon server. Provides position and orientation as a TF or a `geometry_msgs::TransformStamped`. Can also calibrate the origin of an object.

### Kumar Robotics' [motion_capture_system](https://github.com/KumarRobotics/motion_capture_system)

Runs an EKF to provide position, orientation, velocity and angular velocity. Only 1 parameter has to be provided for noise (`max_accel`), can track multiple objects.

We have our own fork on Github [here](https://github.com/MRASL/motion_capture_system).


## Using Matlab/C/C++/.Net
Read the pdf file Vicon_DataStream_SDK_Manual 
