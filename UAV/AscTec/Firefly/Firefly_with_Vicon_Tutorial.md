# Firefly with Vicon Tutorial

## Pre-setup
  * Power on Wireless routers and switches
    * Asus router (WiFi network mrasl)
    * Netgear switch (2 TP-Link Wireless Access Points)
    * 2 Trendnet switches (Vicon cameras)
  * Power on the Firefly
    * Power on the Firefly with an ASCTEC battery fully charged (5000 mAh, 11.1V)
    * Power on the On-Board Computer (OBC)
  * Packages
    * Firefly OBC
      * [asctec_mav_framework](https://github.com/MRASL/asctec_mav_framework): framework for data aquisition and position control to be used with the highlevel processor of Ascending Technologies helicopters.
      * [MSF](https://github.com/ethz-asl/ethzasl_msf): Modular framework for multi sensor fusion based  on an Extended Kalman Filter (EKF).
    * Remote Desktop
      * [VRPN Client](/Equipment/Vicon/Usage): connects to the Vicon server through the Virtual Reality Peripheral Network; provides position, orientation, velocity and angular velocity.
  * Check our [Safety](/UAV/Safety) page

## Vicon
See our [Vicon page](/Equipment/Vicon/Calibration.md) for more detail.
In this tutorial, the object `firefly_blue` is used.

## Remote Computer and Firefly
  * IP address: the remote computer and the firefly have to be connected to the same network (MRASL). The `firefly_blue` IP is then  **[192.168.1.12](/Equipment/Networking/LAN.md)**. For this tutorial assume that the remote computer IP is **192.168.1.4**. You can check your IP address by typing `ifconfig` in a terminal.

  * Remote monitoring and control the Firefly from a distance computer
    *  Check the connectivity between the remote computer and the `firefly_blue`  by running the following command in a terminal:    
```
$ ping 192.168.1.12
```
    * To log into the Firefly's OBC we use the following commands:
```
$ ssh asctec@192.168.1.12
```
This command will open a ssh channel to the `firefly_blue` (default password is `asctec`). If you are using the desktop L5816-18, you can also running the permanent *alias* `$ connect_firefly_blue`.

    * We will use the `firefly_blue` as the ROS master, by setting the **ROS_MASTER_URI** and **ROS_IP** variables to the drone's IP. To change the variables we use the following commands in the remote computer terminal
```
$ export ROS_MASTER_URI=http://192.168.1.12:11311
$ export ROS_IP=192.168.1.4
```
If you are using the desktop L5816-18, you can also running the permanent *alias* `$ master_firefly_blue`.
  * Firefly's OBC
    * If you want to implement your own controller, you should kill the default nodes on OBC by running the following commands in the `firefly_blue` terminal
    ```
    $ rosnode list
    $ rosnode kill /AsctecProc
    $ rosnode kill /AutoPilot
    ```
## Installation the asctec_mav_framework



    * Run the asc_hl_interface
    * Run the msf (filter)

## MSF filter
  * Run from OBC
  * Run from FCU
    * Run VRPN (Vicon)
    * Check data
    * Init the filter from remote computer
    * Verify the filter

## Remote control
