3 Asctec UAV are equipped with an Asctec Mastermind onboard computer (Atom 1.66 GHz dual core CPU, 4 GB RAM), running Ubuntu 14.04 and ROS Jade.

# OBC FAQ
## How can I use the Asctec OBC with a monitor, mouse and keyboard?

*photo here*

## The Astec OBC is not working?
Check BIOS battery

## ROS and/or Ubuntu are broken. How do I recover the factory image and other configurations (from Clearpath Canada)?
* Recovery Image from Astec: Ubuntu and ROS (only core)
* Configure network adapters by typing `sudo vim /etc/network/interfaces` in a terminal, then modify the file as follows
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
    address YOUR_WIRELESS_ADDRESS
    netmask 255.255.255.0
    network YOUR_NETWORK
    gateway YOUR_GATEWAY
    dns-nameservers 8.8.8.8 8.8.4.4
    post-up /sbin/iwconfig wlan0 power off # make sure power management is off --> short ping time
    post-up /sbin/route add -net 192.168.1.0 netmask 255.255.255.0 dev wlan0
```
Example: for Asctec Pelican, YOUR_LAN_ADDRESS is 192.168.1.31, YOUR_WIRELESS_ADDRESS is 192.168.1.21, YOUR_NETWORK is 192.168.1.0, YOUR_GATEWAY is 192.168.1.1, YOUR_SSID is "mrasl" and YOUR_PASSWORD is "saveapril",

  Restart networks:

  ```
  sudo ifdown em1
  sudo ifup em1
  sudo ifdown wlan0
  sudo ifup wlan0
  ```

  Verify new configurations using `ifconfig`.


Notes: [basic Vim syntax](https://www.maketecheasier.com/vim-keyboard-shortcuts-cheatsheet/), Esc => go to command mode, :i => insert text, :w => write file, :q => quit

* ROS dependencies

## How can I sent the individual motor speed commands (lowest command level) to the motor controllers?

* asctec_mav_framework: install, branch, rate, etc (article ICUAS18)
* Flash
* Test
