Parrot AR Drone 1.0 and 2.0
============================

![Image AR Drone](https://www.parrot.com/fr/sites/default/files/styles/product_teaser_hightlight/public/parrot_ar_drone_gps_edition.png?itok=0shlzcXW)

Overview
--------

> Parrot AR.Drone is a remote controlled flying quadcopter helicopter built by the French company Parrot. The drone is designed to be controlled by a mobile device with apps available for iOS and Android or the unofficial software available for Windows Phone, Samsung BADA and Symbian devices.

Wikipedia.

Machines in the Lab
-------------------

There are 4 AR drones in the Lab, including three AR drones 1.0 and one 2.0. The AR drone with the pink hull doesn't work anymore. It seems to be a problem with the ultrasounds.

Getting started
---------------

### Manual flight

To just fly the drone, you need to plug the battery in, wait a short while and connect to the wifi network of the drone (named *ardrone-something*) whith a mobile or tablet. Then the application AR.FreeFlight is userfriendly.

### Control using ROS

To control it with algorithms using ROS, you can download [this ROS package](https://github.com/AutonomyLab/ardrone_autonomy) or install it with this command (by replacing *kinetic* with your own ROS distribution) :

    sudo apt install ros-kinetic-ardrone-autonomy

Then you just need to run this command once you are connected to the drone's network :

    roslaunch ardrone_autonomy ardrone.launch

Then the connection is done. To take off, you just have to publish an empty message on the topic `/ardrone/takeoff` and the same message on the topic `/ardrone/land` to land. In case of emergency, you should stop the motors with the same empty message on the topic `/ardrone/reset`.

You can know the battery charge and more information by subscribing on the topic `/ardrone/navdata`, of type Navdata message (installed in ardrone_autonomy package).

Once the drone has taken off, it hovers. To control it, you can send Twist messages on the topic `/cmd_vel` :

* linear/x to change the pitch,
* linear/y to change the roll,
* linear/z to change the thrust,
* angular/z to change the yaw rate.

You should publish with a rate of at least 50Hz. The range for each component should be between -1.0 and 1.0. I don't really understand why the message is named `cmd_vel` while it is not the velocity that is command. Moreover, you change the pitch by modifying the `linear/x` field of the message, even if the pitch rotates around `y`.

You can find more information [in the documentation of ardrone_autonomy](http://ardrone-autonomy.readthedocs.io/en/latest/).

Using an existing PID controller
--------------------------------

You can use the ROS package [falkor_ardrone](https://github.com/FalkorSystems/falkor_ardrone). To install it, just follow these instructions :

* In your workspace, in the `src` folder, clone the git repository :

    git clone https://github.com/FalkorSystems/falkor_ardrone.git

* Go to the root of your workspace and compile :

    catkin_make

Finally, you just have to publish Twist messages on the topic `/goal_vel` while the `ardrone_control` node is running. To launch it, run this command in a terminal where you have source your workspace (with `source /path/to/your/workspace/devel/setup.bash`) :

    rosrun falkor_ardrone ardrone_control.py
    
So you can control the AR drone with velocity.
