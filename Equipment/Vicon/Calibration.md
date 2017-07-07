# How to Calibrate the Vicon Setup

**Always recalibrate the Vicon **_**every day**_** before starting to work**.

This guide is currently being validated. Please contact [Olivier Gougeon](mailto:olivier.gougeon@polymtl.ca) for comments or suggestions to improve it.

---

## Before You Start

The before-you-start-checklist:

* Is the floor well covered? \(Undesired reflecting surfaces are your \#1 enemy while using the Vicon system!\)
* Are all the objects in the flight area placed in their experimental configuration? \(Mats, tiles, nets, etc.\)
* Am I in a good mood today? \(If not, you might want to consider NOT doing any experimental tests today...\)

If you answered YES to all the questions above, you are now free to proceed to the next step.

---

## \[Partially Optional\] Using the _Vicon Control_ Mobile App

**N.B. Some of the steps provided in this section are specific to the usage of the **_**Vicon Control**_** mobile app and are therefore **_**optional**_**. All of the other steps must be done to be able to use the Vicon system.**

The [_Vicon Control_](https://www.vicon.com/products/software/vicon-control) mobile app is available for iOS or Android devices. You may dowload it visiting the [App Store](https://itunes.apple.com/ca/app/vicon-control/id969977655) or [Google Play](https://play.google.com/store/apps/details?id=com.vicon.control). It allows you do to different things such as playing with the camera and calibration settings. It is mostly useful for the calibration process as it allows you to view directly on your device \(phone or tablet\) and in real-time the advancement of the calibration process underway.

Follow these steps to use the _Vicon Control_ mobile app during the calibration procedure:

1. \[_Optional_\] Connect the black Asus router to the school's network \(use an ethernet cable and link the blue port from the Asus router to the school's acess point located on the wall next to the Vicon computer\)  
   ![](/assets/asus_router_front.jpg)  
   ![](/assets/wall_access_point.jpg)

2. \[_Optional_\] Connect the white UniFi double antenna to the Asus router \(plug the blue ethernet cable from the antenna to one of the available yellow ethernet slots of the Asus router\)  
   ![](/assets/unifi_antenna.jpg)

3. \[_Optional_\] Power on the Asus router \(the switch is located in the back of the router\)  
   ![](/assets/asus_router_back.jpg)

4. \[_Optional_\] The WiFi network _mrasl_ should now be discoverable on your mobile device

5. \[_Optional_\] Login to the _mrasl_ WiFi network using the password that is written on the post-it located on the Asus router

6. Power on the Vicon switches \(connect the two power supply cables\)  
   ![](/assets/poe_switches_front.jpg)![](/assets/poe_switches_back.jpg)

7. Power on the Vicon PC

8. Launch the _Vicon Tracker_ application \(the green shortcut is situated on the desktop\)

   ![](/assets/vicon_shortcut.PNG)

9. Choose the _3D Perspective_ view in the drop-down list  
   ![](/assets/vicon_tracker_3D_perspective.png)

10. Make sure that all of the 12 cameras are green  
    ![](/assets/vicon_tracker_full.png)

11. \[_Optional_\] Open the _Vicon Control_ app on your mobile device

12. \[_Optional_\] Select _Connect Manually_ and enter the following info:  
    1. _Server IP_: 132.207.24.6 \(this is the Vicon's static IP address\)  
    2. _Data Stream Port_: 801  
    3. _Control Stream Port_: 803

13. \[_Optional_\] Click on _Connect_

14. \[_Optional_\] A pop-up should come up on the Vicon PC

15. \[_Optional_\] Clock on _Allow_ to authorize the new connection

16. \[_Optional_\] You are now ready to use the _Vicon Control_ app to navigate through the different camera views \(note that the Vicon system is also ready to be used\)

---

## Calibration Procedure

This section details the calibration procedure of the Vicon system. It is _extremely_ important to calibrate the system _every day_ before doing experimental tests to garantee a millimeter precision. The main reason is that the cameras are mounted on metallic rails that vibrate due to structural stress caused by all the ongoing activities in the university.

Follow these steps to calibrate the Vicon system \(assuming all the previous steps have been completed\):

1. In the _Vicon Tracker_ application, using the drop-down list, navigate to and select:

   ```
   SYSTEM > 12_Cam_Config_Cal
   ```

   ![](/assets/vicon_tracker_100_hz.PNG)

   This is necessary to change the frequency from 250 Hz to 100 Hz in order to obtain better calibration performances.

2. Navigate to and select:  
   `CALIBRATE > CREATE CAMERA MASKS > START`  
   ![](/assets/vicon_tracker_calibration_mask.PNG)

3. Wait a few seconds until all the reflective spots in the flight area become blue \(they are initially white\) and click on _STOP                    
   _**N.B. All the blue spots do no longer belong to the 3D space being monitored by the Vicon system. Make sure that your vehicle will not operate in these **_**dead**_** areas.**

4. Power on the Active Wand and make sure that the 5 lights turn on \(otherwise, you must charge the wand\)  
   ![](/assets/vicon_active_wand.jpg)

5. Navigate to and select:  
   `CALIBRATE > CALIBRATE CAMERAS > START`  
   \`![](/assets/vicon_tracker_calibration_calibrate.PNG)

6. Take the Active Wand and walk in the flight area doing arc-like motions with it over your head. You must pass infront of all the cameras. Make sure that the wand is always visible by at least two cameras.  
   _Recommended:_ Use the Vicon Control app to visualize in real-time the calibration process.

7. When every camera reaches 2000 wand counts, the calibration process automatically stops and the program goes into the final calculation process. If you look at the _3D Pespective_ camera view, you will now see that the orientation of the 3D flight area is all messed up. You must tell the Vicon system what is the new origin after each calibration process.

8. Place the Active Wand in the middle of the flight area _exactly_ like in the following picture:  
   ![](/assets/flight_area.jpg)**N.B. Our lab has adopted the convention that the longest wall is facing the X axis and the shortest the Y axis. The ceiling is facing the Z axis. If you change the orientation of the origin, always make sure that you replace it this way before quitting.**

9. Navigate to and select:  
   `CALIBRATE > SET VOLUME ORIGIN > START`

10. You should see in the _3D Perspective_ camera view that the program has recognized the Active Wand. Cick on \_SET ORIGIN. \_The orientation of the flight area should now be good.

11. Go back to the first step and this time select:  
    `SYSTEM > 12_Cam_Config_250Hz`

12. You are now done with the calibration procedure and the Vicon system is now ready to be used :D



