# Firefly with Vicon Tutorial

## Pre-setup
  * Simulation: successfull test of your own controller on GAZEBO
  * Packages installed
    * Firefly OBC
      * [asctec_mav_framework](https://github.com/MRASL/asctec_mav_framework): framework for data aquisition and position control to be used with the highlevel processor of Ascending Technologies helicopters.
      * [MSF](https://github.com/ethz-asl/ethzasl_msf): Modular framework for multi sensor fusion based  on an Extended Kalman Filter (EKF).
      * Controller: in this tutorial, we will test the [gain-scheduling controller](https://github.com/MRASL/gsft_control)
    * Remote Computer
      * [VRPN Client](/Equipment/Vicon/Usage): connects to the Vicon server through the Virtual Reality Peripheral Network; provides position, orientation, velocity and angular velocity.
  * Power on
    * Asus router (WiFi network mrasl)
    * Netgear switch (2 TP-Link Wireless Access Points)
    * 2 Trendnet switches (Vicon cameras)
    * Power on the Firefly FCU (flight control unit) with an ASCTEC battery fully charged (5000 mAh, 11.1V)
    * Power on the Firefly's On-Board Computer (OBC)
  * Vicon setup: see our [Vicon page](/Equipment/Vicon/Calibration.md) for more detail.

## Network Setup
 Remote monitoring and control the Firefly from a distance computer. In this tutorial, the desktop `L5816-18` and the object `firefly_blue` are used.
  * IP address: the remote computer and the firefly have to be connected to the **same network** (MRASL). The `firefly_blue` IP is 192.168.1.12](/Equipment/Networking/LAN.md)**. For this tutorial assume that the remote computer IP is **192.168.1.4**. You can check your IP address by typing `ifconfig` in a terminal.

  * Remote monitoring and control the Firefly from a distance computer
    *  Check the connectivity between the remote computer and the `firefly_blue`  by running the following command in a remote computer terminal:    
```
$ ping 192.168.1.12
```
    * To log into the Firefly's OBC we use the following commands:
```
$ ssh asctec@192.168.1.12
```
This command will open a ssh channel to the `firefly_blue` (default password is `asctec`). If you are using the desktop `L5816-18`, you can also running the permanent *alias* `$ connect_firefly_blue`.

    * We will use the `firefly_blue` as the ROS master, by setting the **ROS_MASTER_URI** and **ROS_IP** variables to the drone's IP. To change the variables we use the following commands in the remote computer terminal
```
$ export ROS_MASTER_URI=http://192.168.1.12:11311
$ export ROS_IP=192.168.1.4
```
If you are using the desktop `L5816-18`, you can also running the permanent *alias* `$ master_firefly_blue`.

## Before your fly   
  * Setting up the ROS environment: don't forget to run `$ source devel/setup.bash` in each terminal before continue with the following subsections. If you are using the desktop `L5816-18` and the `firefly_blue`, you can also running the permanent *alias* `$ gotien`.

  * Firefly's OBC terminal
    *  If you want to implement your own controller, you should list and kill the default nodes on OBC by running the following commands in the `firefly_blue` terminal
      ```
      $ rosnode list
      $ rosnode kill /AsctecProc
      $ rosnode kill /AutoPilot
      ```
    * Running the Asctec Framework interface and the MSF
    ```
    $ roslaunch asc_hl_interface fcu.launch
    $ roslaunch msf_updates viconpos_sensor.launch
    ```

  * Remote Computer terminal: running the [VRPN Client](/Equipment/Vicon/Usage) node  
  ```
  $ roslaunch ros_vrpn_client mrasl_vicon.launch
  ```
  This launch file is a copy of the original `asl_vicon.launch` with the node name is `xxx` and the param name is `xxx`

# Init the filter
Open a `rqt` GUI in a remote computer terminal by typing `$ rqt`
  * To verify
      * Menu `Plugins/Introspection/Node Graph`: check node
      * Menu `Plugins/Topics/Topic Monitor`: check filter input data and their frequency
        * Data from Vicon: topic `/firefly /xxx`
        * Data from Firefly: topic `/firefly_blue/imu/xxx`

  * Before init the filter
      * Menu `Plugins/Topics/Topic Monitor`: topic `xxx`
      * Menu `Plugins/Visualization/Multiplot`: plot the position, velocity, euler angle and euler rate. If you are using the desktop `L5816-18`, you can open the configuration `xxxx`.

  * Init the filter
    * Menu `Plugins/Configuration/Dynamic Reconfigure`
      * Topic `fcu`: chose `POSCTRL_HL` and `EKF`
      * Topic `core`: click on `core_init_filter`
    * Move the drone and check
      * Message in the Firefly's OBC terminal
      * Data

## Running the demos   
  * Before running the controller
    * RVIZ and RQT
    * Check our [Safety](/UAV/Safety) page
    * Remote control
    * Start the motors

  * Running the controller
    * Running the controller node by typing the following command in a Firefly's OBC terminal
      ```
      $ roslaunch gstf_control lqr_controller.launch
      ```
    * Menu `Plugins/Introspection/Node Graph`: check node
    * **Check the data before active the controller**
    * Active the controller: remote control
    * Send the reference: menu `Plugins/Topics/Message Publisher`
