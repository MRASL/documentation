Our Asctec UAVs are equipped with Asctec Mastermind onboard computers (Atom 1.66 GHz dual core CPU, 4 GB RAM), running Ubuntu 14.04 and ROS Jade.

# OBC Frequenctly Asked Questions
## How can I use the Asctec OBC with a monitor, mouse and keyboard?

*photo here*

## The Astec OBC is not working?
Check BIOS battery

## Wifi keeps dropping out, what gives?
Each UAVs has an Intel 7260 Wifi adapter and there are a lot of complaints online about instability issues. Try adding to `/etc/modprobe/iwlwifi.conf` the following:
```
options iwlwifi 11n_disable=8
```
This should turn on link aggregation and has worked once in the past.

## I'm connected to Wifi but I can't ping anything in the network
Check how you configured your network adapters. Clearpath sent us the UAVs with a static IP on the (always on) ethernet adapter. This allows ROS to work even when not connected to a network. If this IP is on the same subnet as the Wifi adapter, all your packets will go through your unplugged ethernet.

To get around this see our [networking page](/Equipment/Networking/LAN.md) on dealing with multiple interfaces on the same subnet.

* Typing `sudo vim /etc/network/interfaces` in a terminal, then modify this file as follows
```
auto lo
iface lo inet loopback
```
```
auto em1    # LAN
iface em1 inet static
address YOUR_LAN_ADDRESS
```
```
auto wlan0  # WIRELESS
iface wlan0 inet static
    wpa-ssid YOUR_SSID
    wpa-psk YOUR_PASSWORD
    wpa-proto WPA2
    wpa-key-mgmt WPA-PSK
    wpa-ap-scan 1
    wpa-pairwise CCMP
    wpa-group CCMP
    address YOUR_WLAN_ADDRESS
    netmask 255.255.255.0
    network YOUR_NETWORK
    gateway YOUR_GATEWAY
    dns-nameservers 8.8.8.8 8.8.4.4
    post-up /sbin/iwconfig wlan0 power off # make sure power management is off --> short ping time
    post-up /sbin/route add -net 192.168.1.0 netmask 255.255.255.0 dev wlan0
```
  Example: for Asctec Pelican, YOUR_LAN_ADDRESS is 192.168.1.31, YOUR_WLAN_ADDRESS is 192.168.1.32, YOUR_NETWORK is 192.168.1.0, YOUR_GATEWAY is 192.168.1.1, YOUR_SSID is "mrasl" and YOUR_PASSWORD is "saveapril".
* Restart networks:

  ```
  sudo ifdown em1
  sudo ifup em1
  sudo ifdown wlan0
  sudo ifup wlan0
  ```

  Verify new configurations using `ifconfig`. After`sudo reboot`, the LAN and WLAN IP address should be shown in the LCD screen of the UAV.

Notes: [basic Vim syntax](https://www.maketecheasier.com/vim-keyboard-shortcuts-cheatsheet/), Esc => go to command mode, :i => insert text, :w => write file, :q => quit

## ROS and/or Ubuntu are broken. How do I recover the factory image and other configurations (from Clearpath Canada)?
1. [Recovery Image from Astec](http://wiki.asctec.de/display/AR/Recovery+Images)
2. Reconfigure network adapters: see the previous question
3. ROS dependencies: using recovery image from astec, only 'ros-jade-ros-base' is installed.
```
sudo apt install catkin-tools
sudo apt install python-catkin-tools
sudo apt install python-trollius
sudo apt install g++
sudo apt install autoconf
sudo apt install ros-jade-cmake-modules ros-jade-roscpp ros-jade-message-generation
sudo apt install ros-jade-mav-msgs ros-jade-nav-msgs ros-jade-sensor-msgs ros-jade-trajectory-msgs ros-jade-std-msgs ros-jade-geometry-msgs
sudo apt install ros-jade-dynamic-reconfigure
sudo apt update
sudo apt upgrade
sudo reboot
```
Note: from Ubuntu 14, `apt-get` is replaced by `apt`. Use `apt-cache search` for searching apt software packages, e.g. `apt-cache search catkin` => install `python-catkin-tools`.


## How can I sent the individual motor speed commands (lowest command level) to the motor controllers?

1. Install `asctec_mav_framework` and dependencies
  * Clone
  ```
  mkdir -p my_ws/src
  cd my_ws
  catkin build
  cd my_ws/src
  git clone https://github.com/MRASL/asctec_mav_framework
  git clone https://github.com/ethz-asl/ethzasl_msf
  git clone https://github.com/ethz-asl/glog_catkin
  git clone https://github.com/catkin/catkin_simple
  git clone https://github.com/ethz-asl/mav_comm
  ```
  * Create a local branch and checkout the remote branch `origin/direct_motor_ctrl` (our interface for working with direct individual motor control) then build
  ```
  cd asctec_mav_framework
  git checkout -b direct_motor_ctrl origin/direct_motor_ctrl
  catkin build
  cd my_ws
  source devel/setup.bash
  ```
  Note: use `git branch --help` and `git branch --list` for more information.
  * [Change asctec_hl_interface configuration for faster communcation](http://wiki.ros.org/asctec_mav_framework/Tutorials/onboard_computer_setup)
    Downloads this file [09_config_serial](http://wiki.ros.org/asctec_mav_framework/Tutorials/onboard_computer_setup?action=AttachFile&do=view&target=09_config_serial)
    ```
    cd Downloads
    sudo cp 09_config_serial /etc/grub.d
    sudo chmod +x /etc/grub.d/09_config_serial # make it executable
    sudo update-grub # rebuild grub config
    sudo reboot
    ```
    Adjusting the Maximum Baudrate:
    ```
    cd asctec_hl_interface/cfg
    cat HLInterface
    cd asctec_hl_interface/launch
    vim fcu_parameters.yaml
    ```
    Change `fcu/baudrate` to 115200baud and `fcu/packet_rate_imu` to 1000Hz.
2. [Flashing the Higlevel Processor](http://wiki.asctec.de/display/AR/SDK+Setup+for+Linux)
  * Requirements
      * Install OpenOCD
      ```
      sudo apt install openocd
      sudo apt install libncurse5-dev:i386
      sudo apt install libx11-dev:i386
      sudo apt install zlib1g:i386
      ```
      * Install arm-elf-gcc compiler
      ```
      cd asctec_hl_firmware
      ./install_arm7_gcc.h
      export PATH=$PATH:~/Downloads/arm7-elf-gcc/usr/local/arm7/bin
      ```
      Note: `cat install_arm_gcc.h` to view contain of this file
  * Compiling
    ```
    cd asctec_hl_firmware
    make
    ```
    If there are some errors, pls restart the system, `make clean` and `make` again.
  * Flashing
    * Connect OBC (Mastermind) to the Asctec Autopilot via AscTec JTAG Adapter
    * Turn on the Autopilot and check USB port
      ```
      lsusb
      ls -la
      ls -la /dev/ttyUSB*
      ls /dev/ttyUSB0
      ```
    * First terminal:  connect to the device via OpenOCD with the command
      ```
      sudo openocd -f lpc2xxx_asctecusbjtag05.cfg
      ```
      If there are some warnings or errors, please restart the system and try again.
    * Second terminal: open a telnet connection to OpenOCD
      ```
      telnet localhost 4444
      ```
      Then stop, flash and reset the device
      ```
      reset halt
      flash write_image erase main.bin
      reset run
      ```
3. Test

  * Running fcu
    ```
    souce devel/setup.bash
    roslaunch asctec_hl_interface fcu.launch
    ```
  * Sent motor command in range 1 to 200: make sure that the **PROPELLERS ARE NOT MOUNTED**
    ```
    rostopic pub -r 100 /fcu/command/direct_motor mav_msgs/Actuators "header:
      seq: 0
      stamp:
        sec: 0
        nsecs: 0
      frame_id: ''
      angles: -0
      angular_velocities: -0
      normalized: [100, 100, 100, 100, 100, 100]"
    ```

Full experimental system architecture including Vicon system, Ground PC, UAV and networks: read ICUAS18_0164 article.
