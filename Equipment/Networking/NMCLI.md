# NMCLI

## Brief description

`NMCLI` (*Network Manager Command line input*) software is useful to deal with networks without graphic session. We can install it easily typing `sudo apt install nmcli`.

The documentation of this package can be found there : 

https://developer.gnome.org/NetworkManager/stable/nmcli.html

## Getting all useful network information with NMCLI

 To get an exhaustive network information of your device you can type :

`nmcli device show >> "config_reseau_$report$(uname -n).txt"`

If your `hostname` (name of your PC) is `spam` the previous command will produce `config_reseau_l-5816-spam.txt` report. This report is useful when you have to keep the information on another computer. It contains all fields and all internet devices (WiFi and Ethernet) and thus is more exhaustive than simple `ifconfig -a` :

```
`GENERAL.DEVICE:                         enp0s31f6`
`GENERAL.TYPE:                           ethernet`
`GENERAL.HWADDR:                         18:31:BF:30:3B:B1`
`GENERAL.MTU:                            1500`
`GENERAL.STATE:                          100 (connected)`
`GENERAL.CONNECTION:                     Wired connection 1`
`GENERAL.CON-PATH:                       /org/freedesktop/NetworkManager/ActiveConnection/1`
`WIRED-PROPERTIES.CARRIER:               on`
`IP4.ADDRESS[1]:                         132.207.24.13/24`
`IP4.GATEWAY:                            132.207.24.1`
`IP4.ROUTE[1]:                           dst = 0.0.0.0/0, nh = 132.207.24.1, mt = 100`
`IP4.ROUTE[2]:                           dst = 132.207.24.0/24, nh = 0.0.0.0, mt = 100`
`IP4.ROUTE[3]:                           dst = 169.254.0.0/16, nh = 0.0.0.0, mt = 1000`
`IP4.DNS[1]:                             132.207.136.10`
`IP4.DNS[2]:                             132.207.136.11`
`IP4.DNS[3]:                             132.207.6.11`
`IP4.DNS[4]:                             132.207.6.12`
`IP4.DOMAIN[1]:                          ge.polymtl.ca`
`IP6.ADDRESS[1]:                         fe80::1a31:bfff:fe30:3bb1/64`
`IP6.GATEWAY:                            --`
`IP6.ROUTE[1]:                           dst = ff00::/8, nh = ::, mt = 256, table=255`
`IP6.ROUTE[2]:                           dst = fe80::/64, nh = ::, mt = 256`

`GENERAL.DEVICE:                         wlp3s0`
`GENERAL.TYPE:                           wifi`
`GENERAL.HWADDR:                         E8:2A:44:C2:8E:E3`
`GENERAL.MTU:                            1500`
`GENERAL.STATE:                          20 (unavailable)`
`GENERAL.CONNECTION:                     --`
`GENERAL.CON-PATH:                       --`

`GENERAL.DEVICE:                         lo`
`GENERAL.TYPE:                           loopback`
`GENERAL.HWADDR:                         00:00:00:00:00:00`
`GENERAL.MTU:                            65536`
`GENERAL.STATE:                          10 (unmanaged)`
`GENERAL.CONNECTION:                     --`
`GENERAL.CON-PATH:                       --`
`IP4.ADDRESS[1]:                         127.0.0.1/8`
`IP4.GATEWAY:                            --`
`IP6.ADDRESS[1]:                         ::1/128`
`IP6.GATEWAY:                            --
```

