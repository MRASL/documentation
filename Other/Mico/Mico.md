# Kinova Mico Arm

## Hardware

The lab owns a Mico 6DoF arm from [Kinova Robotics](http://www.kinovarobotics.com/innovation-robotics/products/robot-arms/) here in Quebec. It was purchased to be mounted onto the Husky robot.

Look for a black protective case that looks like this.

![](/assets/images/kinova_mico/mico_case.jpg)

Inside you'll find the arm (middle), the manual controller (bottom left) and the power supply (top right).

![](/assets/images/kinova_mico/mico.jpg)

If you want to mount it on the Husky, there is a little nub of extruded aluminum at the from right of it.

![](/assets/images/kinova_mico/husky_mico_mount.jpg)

To power the arm from the Husky:

1. Connect the 4 pin barrel jack to 4 pin Molex adapter to the arm ![](/assets/images/kinova_mico/husky_power.jpg)
1. Connect the adapter to an internal 4 pin Molex labeled as "ARM" in the husky ![](/assets/images/kinova_mico/husky_connector.jpg)

## Software

An official [ROS driver](git@github.com:Kinovarobotics/kinova-ros.git) implementation is available from Kinova.

## Important considerations

* **Read the manual** before using the arm. It contains important instructions on how to operate the arm and use the controller.