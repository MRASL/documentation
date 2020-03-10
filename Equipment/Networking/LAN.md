# MRASL's Local Area Network

![](/assets/images/equipment/mrasl_lan.png)

## Quick explanation
Polytechnique put the lab in the `132.207.24.0` subnet. Since were not allowed to plug a router to the school's network we built our own local network in `192.168.1.0`. This network is composed of two TP-Link EAP220 access points and one Asus RT-AC55U which also acts as the DHCP server. Lucky for us, the Vicon server shipped with an extra network interface card with 4 ports, therefore we can connect it to the Vicon network `192.168.10.0`, the lab network `132.207.24.0` and the local wireless network `192.168.1.0`.

Each aerial vehicle has an always on ethernet interface and a wireless interface, both with static addresses. I believe Clearpath made the ethernet interfaces always on and with static IPs to make it easier to network multiple vehicles and for ROS to work right with and without a network.

## IP Address Allocation
The following table shows the static ip addresses on the network. If you add equipment in the lab with a static address on the network, please update the table.

| Address             | Usage                                 |
|---------------------|---------------------------------------|
| 192.168.1.1         | Asus Router                           |
| 192.168.1.2         | EAP220                                |
| 192.168.1.3         | EAP220                                |
| 192.168.1.\[4-10\]    | **Reserved for future network equipment** |
| 192.168.1.11        | AscTec Firefly Blue (wired)           |
| 192.168.1.12        | Asctec Firefly Blue (wireless)        |
| 192.168.1.13        |  *Unused*                             |
| 192.168.1.14        | Parrot AR Drone 1.0                   |
| 192.168.1.15        | Parrot AR Drone 1.0                   |
| 192.168.1.16        | Parrot AR Drone 2.0                   |
| 192.168.1.\[17-20\]   | *Unused*                                |
| 192.168.1.21        | AscTec Firefly Green (wired)          |
| 192.168.1.22        | AscTec Firefly Green (wireless)       |
| 192.168.1.\[23-30\]   | *Unused*                                |
| 192.168.1.31        | AscTec Pelican Red (wired)            |
| 192.168.1.32        | AscTec Pelican Red (wireless)         |
| 192.168.1.\[33-99\]   | *Unused*                                |
| 192.168.1.100       | AscTec Pelican Red (Hokuyo lidar)     |
| 192.168.1.\[101-199\] | *Unused*                                |
| 192.168.1.200       | Vicon Server                          |
| 192.168.1.\[201-254\] | *Unused*                               |

## Dealing with multiple interfaces on the same subnet
If you're setting up a vehicle with two network interfaces on the same subnet just like the AscTec MAVs you might find yourself unable to connect to the network e.g. if `em1` and `wlan0` are up but the ethernet cable is disconnected. The reason is that Ubuntu will prioritize going through the wired interface. You can force Ubuntu to use the `wlan0` interface by adding a network route:
```
route add -net 192.168.1.0 netmask 255.255.255.0 dev wlan0
```
You can even add this route in the network interface configuration in `/etc/network/interfaces` for example:
```
auto wlan0
iface wlan0 inet static
  wpa-ssid "YOUR_SSID"
  wpa-psk "YOUR PASSWORD"
  wpa-proto WPA2
  wpa-key-mgmt WPA-PSK
  wpa-ap-scan 1
  wpa-pairwise CCMP
  wpa-group CCMP
  address YOUR_ADDRESS
  netmask 255.255.255.0
  network YOUR_NETWORK
  gateway YOUR_GATEWAY
  dns-nameservers 8.8.8.8 8.8.4.4
  post-up /sbin/route add -net 192.168.1.0 netmask 255.255.255.0 dev wlan0
```

