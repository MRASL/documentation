# How to Calibrate the Vicon Setup

**Always recalibrate the Vicon **_**every day**_** before starting to work**.

Ask [Olivier Gougeon](mailto:olivier.gougeon@polymtl.ca) how to calibrate.

**\[WHAT FOLLOWS IS CURRENTLY BEING EDITED\]**

## Before You Start

The before-you-start-checklist:

* Is the floor well covered? \(Undesired reflecting surfaces are your \#1 enemy while using the Vicon system!\)
* Are all the objects in the flight area placed in their experimental configuration? \(Mats, tiles, nets, etc.\)
* Am I in a good mood today? \(If not, you might want to consider NOT doing any experimental tests today...\)

If you answered YES to all the questions above, you are now free to proceed to the next step.

## \[Optional\] Using the _Vicon Control_ Mobile App

The [_Vicon Control_](https://www.vicon.com/products/software/vicon-control) mobile app is available for iOS or Android devices. You may dowload it visiting the [App Store](https://itunes.apple.com/ca/app/vicon-control/id969977655) or [Google Play](https://play.google.com/store/apps/details?id=com.vicon.control). It allows you do to different things such as playing with the camera and calibration settings. It is mostly usefull for the calibration process as it allows you to view directly on your device \(phone or tablet\) and in real-time the advancement of the calibration process underway.

Follow these steps to use the _Vicon Control_ mobile app during the calibration process:

1. Connect the black Asus router to the school's network \(use an ethernet cable and link the blue port from the Asus router to the school's acess point located on the wall next to the Vicon computer\)  
   ![](/assets/asus_router_front.jpg)  
   ![](/assets/wall_access_point.jpg)

2. \[Optional\] Connect the white UniFi double antenna to the Asus router \(plug the blue ethernet cable from the antenna to one of the available yellow ethernet slots of the Asus router\)  
   ![](/assets/unifi_antenna.jpg)

3. Power on the Asus router \(the switch is located in the back of the router\)  
   ![](/assets/asus_router_back.jpg)

4. The WiFi network _mrasl_ should now be discoverable on your mobile device

5. Login to the _mrasl_ WiFi network using the password that is written on the post-it located on the Asus router

6. Power on the Vicon switches \(connect the two power supply cables\)  
   ![](/assets/poe_switches_front.jpg)![](/assets/poe_switches_back.jpg)

7. Power on the Vicon PC

8. Launch the _Vicon Tracker_ application \(the green shortcut is situated on the desktop\)  
  
   ![](/assets/vicon_shortcut.PNG)

9. Choose the _3D Perspective_ view in the drop-down list  
   ![](/assets/vicon_tracker_3D_perspective.png)

10. Make sure that all of the 12 cameras are green  
    ![](/assets/vicon_tracker_full.png)

11. Open the _Vicon Control_ app on your mobile device

12. Select _Connect Manually_ and enter the following info:  
    1. _Server IP_: 132.207.24.6 \(this is the Vicon's static IP address\)  
    2. _Data Stream Port_: 801  
    3. _Control Stream Port_: 803

13. Click on _Connect_
14. A pop-up should come up on the Vicon PC
15. Clock on _Allow_ to authorize the new connection



