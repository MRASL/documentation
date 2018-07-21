# Frequently Asked Questions

## Why can't I see the local network MRASL WiFi Network from my personnal laptop?
[MRASL's Wifi Network](/Equipment/Networking/WiFi.md) is only on the 5GHz band. Please check if your laptop supports it and how to enable 5GHz.

## My labtop connected to the local network MRASL. Why can't it receive data from VICON server (192.168.1.200)?
  * Check the Asus router (local network MRASL) connections
    *photo here*
  **N.B. Do not connect this router to the school's network (prohibited by the Service Informatique Polymtl)!**

  * Check the Vicon server network connections: *MRASL LAN* - local network connection, *Polymtl Internet* - school's network and *VICON MX* - 12 cameras
    *photo here*

  * Check network adapter priorities:
    * Remove all network connections.
    * Connect the Vicon server to the school's network. You should have Internet via *Polymtl Internet*.
    * Connect the Vicon server to the Asus router. If there is no Internet, it means *MRASL LAN* connection has more priority than *Polymtl Internet* connection.

  * Change network adapter priorities: *MRASL LAN* connection has to have **less priority** than *Polymtl Internet* connection.
    1. Goto Control Panel > Network and Internet > Network Connections
    2. Right click the *Polymtl Internet* connection (Higher Priority Connection)
    3. Click Properties > Internet Protocol Version 4
    4. Click Properties > Advanced
    5. Uncheck 'Automatic Metric'
    6. Enter 10 in 'Interface Metric'
    7. Click OK
    Repeat for the *MRASL LAN* connection (Lower Priority Connection), but this time put 20 into the 'Interface Metric'.

## How can I check the connection between my personnal laptop and the Vicon server via MRASL's local network?
  * Connect your laptop (wire/wireless) and the Vicon server (wire) to the MRASL's local network.
  * Vicon server: run Vicon tracker 3.4
  * Personnal laptop:
    * Install
    * Run 
  * Power on the Active Wand and walk in the flight area. You should
