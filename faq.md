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
1. Check Vicon cameras using Vicon Control mobile app: see our [Vicon page](/Equipment/Vicon/Calibration.md)
2. Check Vicon data and connection using Vicon DataStream SDK
  * Connect your laptop (wire/wireless) and the Vicon server (wire) to the MRASL's local network.
  * Vicon server: run Vicon tracker 3.4
  * Personnal laptop:
    * Install Vicon DataStream SDK
    * Open a terminal and go to the installed folder (C:\Program Files\Vicon\DataStream SDK\Win64\SimpleViewer) and run the SimpleViewer application
      ```      
      ViconDataStreamSDK_SimpleViewer.exe 192.168.1.200
      ```
      If the connection to the Vicon server (192.168.1.200) is well established,  the SimpleViewer interface will be opened.

      ![](/assets/ViconSDK.png)   
  * Power on the Active Wand and walk in the flight area. You can see the Active Wand object in the SimpleViewer interface. The Vicon data is now ready to be used in your personnal laptop.

## How can I get the Vicon data?
Visit [Vicon page](/Equipment/Vicon/Usage.md)

## Can I access the Vicon data from the eduroam or robots wifi networks?
To our knowledge no. You must plug in through ethernet in the local network or through a wireless router connected to the local network. The reason is that there is a firewall between our subnet and the `robots` network. We've been told by an IT guy that we can ask them to open some ports for us to get ssh and vicon data to passthrough. We are still reviewing this option.

## Do I really need to cover the floor before using mocap?
Yes. The floor is far too reflective and creates lots of noise in the Vicon data. Ideally also get rid of/cover up metallic objects that can reflect infrared light.

## How many markers do I need to put on my vehicle for it to be recognized as an object?
Minimum 3, try to space them out on all axes and place them in a non-symmetric pattern. Ideally in a way that the markers are all visible from every viewpoint.

## What if I have a question that no one in the lab can answer?
Our point of contact is Felix Tsui (he installed the cameras in the lab) his contact information is taped on top of the server.
