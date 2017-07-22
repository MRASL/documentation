# WiFi equipment
> **Info** July 22nd 2017 there will soon be a new wifi setup with two TP-Link EAP220 access points ceiling mounted in the flight area. More info to come as it is setup. We might even keep the Asus router in the network just for extra redundancy.

The lab has the following Wifi equipment:

* Asus RT-AC55U (or similar) Dual band router
* Ubiquity Unifi AP Outdoor 2.4Ghz
* Ubiquity AirMax Omnidirectional 2x2 antenna 2.4Ghz (high gain)

## Internal setup
As of April 10th 2017 we have the Asus router on channel 165 of the 5Ghz band with the ssid `mrasl`. Talk to Andre for the password. The school doesn't use channel 165 so it should be free of interference.

## General notes on usage

* Always shutdown wifi equipment when you're done with it. Technically we aren't allowed to operate our own WiFi network.
* For some reason, the Asus router's wifi connection is a bit flimsy. We usually simply use it as a router.
* For a good connection **both** sides must have high gain/high power wireless adapters. That means that if you want to take full advantage of the Ubiquity equipment, you'll have to have another Unifi adapter on the other side.

## Notes on WiFi rules at school

The IT department is actually pretty strict about student not interfering with the wireless network at school. Here are the guidelines they sent us:

* We can have a router on the 5Ghz band if we're on channel 165. This is only possible if you set the channel bandwidth to 20 Mhz.
* We can **not** have a router on the 2.4Ghz band.

There exists an unprotected network with the SSID `Robots` at school made for robots and any kind of device needing to connect to the network without proper authentification. It works by MAC address whitelisting so you need to ask the IT department to add your MAC address to the list.
