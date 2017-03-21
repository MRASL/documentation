# Clearpath Husky

## Onboard Equipment

* [MicroStrain 3DM GX3-25](http://www.microstrain.com/inertial/3dm-gx3-25)
* [Point Grey Bumblebee BB2 Stereo Camera](https://www.ptgrey.com/bumblebee2-firewire-stereo-vision-camera-systems)
* [NovAtel SMART6-L 2 cm L1/L2 GPS unit](http://www.novatel.com/products/smart-antennas/smart6-l/)
* [Axis P5512e PTZ Dome Camera](https://www.axis.com/ca/en/products/axis-p5512-e)
* [SICK LMS511 LIDAR](https://www.sick.com/ca/en/product-portfolio/fluid-sensors/flow-sensors/bulkscan-lms511/c/g253553)
* Asus Wi-Fi Router
* Mini-Itx computer

## Network Configuration

| Parameter                   | Robot               |
| -------------               | -------             |
| Router IP                   | 192.168.1.10        |
| Login                       | *****               |
| 2.4GHz SSID                 | PLM_Husky           |
| 5.0GHz SSID                 | PLM_HUSKY_5G        |
| Password                    | *****               |
| Onboard computer IP         | 192.168.1.11        |
| Onboard computer Hostname   | cpr-plm01-husky     |
| Onboard computer login      | *****               |
| Axis camera IP              | 192.168.1.14        |
| Axis PTZ camera Login       | ******              |
| SICK Lidar IP               | 192.168.1.14        |

**\*** Talk to Andre about this


## Spare Parts

There isn't much available to us in terms of spare parts. The storage cabinets
have a few spare fuses at different ratings. DO NOT change the fuse rating (5A) on
the 5V, 12V and 24V rails. Theses fuses are accessible in the fuse panel in the
battery compartment. The higher amp fuses are meant to be placed in line with high
loads connected directly to the battery.

## Custom modifications by Clearpath

To supply power to the Kinova Mico Arm, Clearpath added a relay that closes once
the onboard DC/DC converters power up. The relay connects the arm directly to
the battery.

## Custom modificatons by MRASL

In order to supply power to a Microsoft Kinect 2 during S.R. Manikandasriram's
mapping project, an extra isolated 12V rail was required.
