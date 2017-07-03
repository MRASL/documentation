# **Crazyflie 2.0**

![](/assets/crazyflie 2.0.jpg)

#### Overview

The Crazyflie 2.0 is an open-source micro-quadrotor created by Bitcraze. It can be controlled with a remote control device using a premade client or by an external program via the crazyradio PA dongle. For more information on the specifications of the crazyflie 2.0 see Ben Landry's Master's thesis: 

[http://groups.csail.mit.edu/robotics-center/public\_papers/Landry15.pdf](http://groups.csail.mit.edu/robotics-center/public_papers/Landry15.pdf)

In its default settings, the crazyflie 2.0 accepts the following types of commands:

* Commanded Thrust in PWM \( values between 0-65535\) 
* Commanded pitch angle in degrees
* Commanded roll angle in degrees
* Commanded yaw **RATE** in degrees/sec

Note that if the controller you've designed controls for individual rotor speeds, you'll have to either restructure your controller or completely rework the quad's firmware \(possible but complicated and might produce limited results. more on that later\). 

When Communicating with R.O.S. It returns:

* Commanded individual rotor speeds
* Yaw,Pitch Roll rates and angles in deg/sec and deg

Unfortunately it does not automatically return the values of the other on-board accelerometers and gyros that could be useful in the estimation of the position and velocity of the quadrotor. 

## Getting Started

The Bitcraze website has some very useful pages and tutorials when you're starting out with the crazyflie 2.0. They can be found here:

[https://www.bitcraze.io/start](https://www.bitcraze.io/start/)

Some useful topics include:

* [Getting started with the Crazyflie 2.0](https://www.bitcraze.io/getting-started-with-the-crazyflie-2-0/) \(for installation of the client, virtual machine\)

* [Getting started with development](https://www.bitcraze.io/getting-started-with-development/) \(for firmware modifications\)

# More to come... 







