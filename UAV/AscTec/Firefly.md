The green firefly has been flashed with a special firmware on the high level containing a Luenberger observer fusing incoming pose information with the onboard IMU. This allows `firefly_green` to be controlled using the Vicon system.

The `firefly_blue` still has stock firmware.

<iframe width="560" height="315" src="https://www.youtube.com/embed/cFhYZdTYz7s" frameborder="0" allowfullscreen></iframe>

# Operating the Asctec Firefly

Start here: http://wiki.asctec.de/display/AR/User+Manual

# Frequenctly Asked Questions

## Wifi keeps dropping out, what gives?
The firefly has an Intel 7260 Wifi adapter and there are a lot of complaints online about instability issues. Try adding to `/etc/modprobe/iwlwifi.conf` the following:
```
options iwlwifi 11n_disable=8
```
This should turn on link aggregation and has worked once in the past.

## I'm connected to Wifi but I can't ping anything in the network
Check how you configured your network adapters. Clearpath sent us the Fireflys with a static IP on the (always on) ethernet adapter. This allows ROS to work even when not connected to a network. If this IP is on the same subnet as the Wifi adapter, all your packets will go through your unplugged ethernet.

Currently the only workaround we know of is to have both adapters on different subnets e.g. `192.168.2.xxx` and `192.168.1.xxx`.
