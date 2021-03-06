# **Crazyflie 2.0**

<figure>
  <img width="45%" src="/assets/crazyflie 2.0.jpg" />
</figure>

## Overview

The Crazyflie 2.0 is an open-source micro-quadrotor created by Bitcraze. It can be controlled with a remote control device using a premade client or by an external program via the crazyradio PA dongle. For more information on the specifications of the crazyflie 2.0 see Ben Landry's Master's thesis:

[Planning and Control for Quadrotor Flight through Cluttered Environments](http://groups.csail.mit.edu/robotics-center/public_papers/Landry15.pdf)

In its default settings, the crazyflie 2.0 accepts the following types of commands:

*   Commanded Thrust in PWM \( values between 0-65535\) 
*   Commanded pitch angle in degrees
*   Commanded roll angle in degrees
*   Commanded yaw **RATE** in degrees/sec

tests have shown that the equilibrium value of thrust for the crazyflie in steady hover is 38160.

Note that if the controller you've designed controls for individual rotor speeds, you'll have to either restructure your controller or completely rework the quad's firmware \(possible but complicated and might produce limited results. more on that later\).

When Communicating with R.O.S. it returns:

*   Commanded individual rotor speeds
*   Yaw, Pitch Roll rates and angles in deg/sec and deg

Unfortunately it does not automatically return the values of the other on-board accelerometers and gyros that could be useful in the estimation of the position and velocity of the quadrotor.

## Machines in the Lab

There are 3 crazyflies in the lab.

Please note that the barometer sensor of one of them \(identificator?\) dosn't work anymore. If you use it with the official firmware, the self-tests that are automatically launched when you power on the crazyflie will fail, because of this dysfunctional sensor. However, it is possible to use it anyway, by bypassing the defective sensor. There is a firmware which do that, you can find more information in the "Possible Firmware Mods" section, below.

## Getting Started

The Bitcraze website has some very useful pages and tutorials when you're starting out with the crazyflie 2.0. They can be found here:

[https://www.bitcraze.io/start](https://www.bitcraze.io/start/)

Some useful topics include:

*   [Getting started with the Crazyflie 2.0](https://www.bitcraze.io/getting-started-with-the-crazyflie-2-0/) \(for installation of the client, virtual machine\)
*   [Getting started with development](https://www.bitcraze.io/getting-started-with-development/) \(for firmware modifications\)

If you're working in Ubuntu, you will need to set up a udev rule giving read/write permissions to the crasyradio USB dongle. This will allow communications between the crazyflie 2.0 and your P.C. Useful links for writing these permissions can be found here:

*   [Writing Udev Rules](http://weininger.net/how-to-write-udev-rules-for-usb-devices.html "writing udev rules")
*   [Using the Vim Text Editor](https://coderwall.com/p/adv71w/basic-vim-commands-for-getting-started)

## Setting up With ROS

If you want to control your crazyflie over ROS, there are a few steps you must follow. If you are unfamiliar with ROS, please see the section dedicated to it in the Software section of the documentation or go through some base tutorials:

[http://wiki.ros.org/ROS/Tutorials](http://wiki.ros.org/ROS/Tutorials)

You can download [this ROS package](https://github.com/whoenig/crazyflie_ros.git) and install it to communicate with the drone.

Once it is installed in a ROS workspace, and you have `source devel/setup.bash`the package in a terminal, you must launch a server before starting the communication with this command :

    roslaunch crazyflie_driver crazyflie_server.launch

While it is running, in another terminal (still with the `source` command), run this command to start communicating with your crazyflie :

    roslaunch crazyflie_driver crazyflie_add.launch 

If you need to select the crazyflie you want to communicate with, you should precise the uri parameter :

    roslaunch crazyflie_driver crazyflie_add.launch uri:=radio://0/80/2M

You can find this information by clicking the `scan` button in the [cfclient](https://github.com/bitcraze/crazyflie-clients-python).

At this step, you are connected with the drone, and you can check the voltage of the battery by subscribing on the `/battery` ROS topic (of type Float32). You can also publish a Twist message on the `cmd_vel` topic to change the angles and the thrust. Yes, you change the euler angles with a velocity command, I don't understand why. Anyway, you can publish the message following this instructions :

*   linear.x: pitch \[e.g. -30 to 30 degrees\]
*   linear.y: roll \[e.g. -30 to 30 degrees\]
*   linear.z: thrust \[10000 to 60000 (mapped to PWM output)\]
*   angular.z: yawrate \[e.g. -200 to 200 degrees/second\]

The thrust level you should publish to hover is around 39000.

.......

## Possible Firmware Mods

*   individual motor control......
*   accelerometer reading for EKF......
*   Changing attitude controller gains.....

### Bypassing the Barometer Sensor

You can download [this firmware](https://forum.bitcraze.io/download/file.php?id=403) and update it in the crazyflie to bypass the barometer sensor and use a crazyflie with a defective sensor.

......

# More to come...
