# WiFi equipment
The lab has the following Wifi equipment:

* 1 x Asus RT-AC55U Dual band router
* 2 x TP-Link EAP220
* 1 x Ubiquity Unifi AP Outdoor 2.4Ghz
* 1 x Ubiquity AirMax Omnidirectional 2x2 antenna 2.4Ghz (high gain)

## Internal setup
See the [LAN page](Equipment/Networking/LAN.html). Our WiFi network is only on the 5Ghz band to prevent interference with RC receivers and XBee chips. To turn it on, power up the switch with the red ethernet wires and the Asus router.

## Outdoor setup
The Ubiquiti Antenna and access points are meant to be deployed in outdoor operations when wireless networking is required between a ground station and a drone. You'll probably need a router to act as a dhcp server.

## General notes on usage

* Always shutdown wifi equipment when you're done with it. Technically we aren't allowed to operate our own WiFi network.
* For some reason, the Asus router's wifi connection is a bit flimsy. We usually simply use it as a router.
* For a good connection **both** sides must have high gain/high power wireless adapters. That means that if you want to take full advantage of the Ubiquity equipment, you'll have to have another Unifi adapter on the other side.

## Notes on WiFi rules at school

The IT department is actually pretty strict about student not interfering with the wireless network at school. Here are the guidelines they sent us:

* We can have a router on the 5Ghz band if we're on channel 165. This is only possible if you set the channel bandwidth to 20 Mhz.
* We can **not** have a router on the 2.4Ghz band.

There exists an unprotected network with the SSID `Robots` at school made for robots and any kind of device needing to connect to the network without proper authentification. It works by MAC address whitelisting so you need to ask the IT department to add your MAC address to the list.
