# Firefly with Vicon Tutorial

## Pre-setup
  * Power on Wireless routers and switches
    * Asus router (WiFi network mrasl)
    * Netgear switch (2 TP-Link Wireless Access Points)
    * 2 Trendnet switches (Vicon cameras)
  * Firefly
    * Power on the Firefly with an ASCTEC battery fully charged (5000 mAh, 11.1V)
    * Power on the OBC (On-Board Computer)

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
This command will open a ssh channel to the `firefly_blue`.

  * Remote Computer
    * We will use the `firefly_blue` as the ROS master, by setting the **ROS_MASTER_URI** and **ROS_IP** variables to the drone's IP. To change the variables we use the following commands in the remote computer terminal
```
$ export ROS_MASTER_URI=http://192.168.1.12:11311
$ export ROS_IP=192.168.1.4
```
  * Firefly's OBC
    * Kill default nodes on OBC
    * Run the hl_interface
    * Run the msf (filter)

## MSF filter
  * Run from OBC
  * Run from FCU
    * Run VRPN (Vicon)
    * Check data
    * Init the filter from remote computer
    * Verify the filter

## Remote control
