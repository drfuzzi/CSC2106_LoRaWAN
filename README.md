# LoRaWAN Lab

## Objectives
-	To understand the core components in a LoRaWAN IoT solution.
-	To understand the process in setting up a fully LoRaWAN-compliant IoT solution, using Cytron LoRa-RFM Shield + Cytron UNO as an end-device, and RAK WisGate Edge Lite 2 as gateway.


## Equipment
-	RAK7268/RAK7268C WisGate Edge Lite 2
-	Ethernet Cable (RJ-45 Port) – for Ethernet Connection
-	Cytron UNO
-	Cytron LoRa-RFM Shield
-	USB Micro B Cable
-	A Windows/macOS/Linux computer


## Introduction
LoRaWAN is a protocol based on an open-source specification developed by Semtech. LoRaWAN protocol leverages the unlicensed radio spectrum in the Industrial, Scientific, and Medical (ISM) band. The specification defines the device-to-infrastructure of LoRa physical layer parameters and the LoRaWAN protocol and provides interoperability between devices. 

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/2777ad1b-4bac-4ab6-9258-2e5235a445ca)
Figure 1: LoRa-RFM + UNO (End Device)

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/9e3b5763-1795-40fc-8bb3-373d845d4ce7)
Figure 2: WisGate Edge Lite (Gateway)

In short, LoRaWAN is an example of a low power wide area network that is based on LoRa radio modulation. While Semtech provides the LoRa radio chips, the LoRa Alliance, drives the standardization and harmonization of the LoRaWAN protocol. 

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/1055b93c-431e-4b13-a4f0-486cd3d9a21d)
Figure 3: LoRaWAN Architecture

The architecture of a LoRaWAN network is shown above. 

-	End devices (nodes): Transmit their payloads in what is known as an uplink message, to be picked up by a LoRaWAN gateway. A key aspect of LoRaWAN is that a device is not associated with a single gateway and its payloads may be picked up by any number of LoRaWAN gateways within the device’s range. 
- Gateway: Pass messages to its associated LoRaWAN network server (LNS), usually carried out over Wi-Fi or Ethernet. Cellular and satellite gateways are available to enable very remote solutions without relying on an internet connection. There are various options for network servers, for example The Things Network (TTN). The LNS receives the messages from the gateway and checks whether the device is registered on its network; the LNS also carries out decoupling, since the message may be received and uploaded by multiple gateways. The message is then forwarded to the application server on which the device is registered. 

Communication is also possible in the other direction, where a message is sent as a downlink to the node. The downlink message is sent from the application server to the network server. The network server then queues the downlink, and when the device next sends an uplink message, the network server will pass the downlink message to the nearest gateway which received the uplink. The gateway then broadcasts the downlink message for the device to receive. Common uses for a downlink message are to update a device’s broadcast settings (i.e. updates more/less frequent) or trigger some other action (e.g. causing a device to open/close or turning the power on/off).



## Lab Exercise

In this exercise, we will use the LoRa-RFM + UNO as the end device communicating to the WisGate Edge Lite as the gateway. And subsequently, via the IP network, platform such as TheThingsNetwork acts as the network server to manage the gateways, end-devices, applications. It also acts as the Application Server processing application-specific data messages received from end devices.
Ensure that the Maker UNO is connected to the Cytron LoRa-RFM Shield, as shown below.

### Gateway Setup (for reference, skip for in-lab exercise)
1. **Attach the LoRa Antenna**

First and foremost, screw on the antenna to the RP-SMA connector on the back panel of the RAK7268/C WisGate Edge Lite 2.

**WARNING**: Do not power the device if the LoRa Antenna port has been left open to avoid potential damage to the RAK7268/RAK7268C WisGate Edge Lite 2.

2. **Power the gateway ON**

It is recommended to use the 12 V DC adapter that comes with the RAK7268/RAK7268C WisGate Edge Lite 2. Optionally, you can use your own PoE cable and injector since the device supports PoE.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/856cd97c-a247-4530-998b-b41902288c32)
Figure 4a: RAK7268/C WisGte Edge Lite 2 Top View            

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/11a64b0d-ec89-45de-b887-aa6e29d6bb70)
Figure 4b: RAK7268/C WisGate Edge Lite 2 Back Panel


### Gateway Configuration (for reference, skip for in-lab exercise)

1. **Access the Gateway**

In this section, several ways of accessing the gateway are provided to have different alternatives for you to choose from depending on the availability of the requirements needed.

**WARNING**: Do not power the device if the LoRa Antenna port has been left open to avoid potential damage to the RAK7268/RAK7268C WisGate Edge Lite 2.

**Wi-Fi AP Mode**

By default, the gateway will work in Wi-Fi AP Mode which means that you can find an SSID named RAK7268_XXXX on your PC’s Wi-Fi Network List. XXXX is the last two bytes of the gateway’s MAC address.

No password is required to connect via Wi-Fi
Using your preferred Web browser, log in with the credentials provided below:

-	Browser Address: 192.168.230.1
-	Username: root
-	Password: admin12345678!

**NOTE**: Please do not change the password. 

**WAN Port (Ethernet)**

Connect the Ethernet cable to the port marked ETH on the gateway and the other end to the PoE port of the PoE injector. Connect the LAN port of the PoE injector to your PC. The default IP is 169.254.X.X. The last two segments (X.X) are mapped from the last four bits of the MAC address of your gateway. For example, the last four bits of the MAC address are 0F:01, and the IP address is 169.254.15.1. Make sure to manually set the address of your PC to one in the same network (for example 169.254.15.100). Use the same credentials for the Web UI as for AP mode.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/2f2cfbc9-707d-43ae-8fdf-d0f1976de236)
Figure 5: Wisgate - Web UI Login Page

2. **Access the Internet**

**Connect through Wi-Fi**

Go into the Network>Wi-Fi->Settings 

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/e06226e9-eb62-45cd-9bae-e8cc46f0abd8)
Figure 6: Wisgate- WiFi Menu Page

Select DHCP Client in the Mode field. Enter or click “Scan” to choose your ESSID, select the right Encryption method and enter the correct Key.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/7da5bf31-818e-406f-ab25-23e2f2b8bdc2)
Figure 7: Wisgate - Connect through Wi-Fi Credentials

**NOTE**: Assuming you have entered the correct parameter values you should get an IP address assigned by your Wi-Fi router’s (AP) built-in DHCP server. You can use this new IP address to log in via a web browser (same way as in AP mode).

3. **Setup Gateway with TTN Credentials**

-	Select Work mode as “Packet forwarder”.
-	Enter Server URL as “au1.cloud.thethings.network”.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/dae28949-6f4d-4952-8603-0fd4a73bd18d)
Figure 8: Wisgate – Packet Forwarder Mode

### Gateway Configuration with The Things Network (for reference, skip for in-lab exercise)

1. Set up account with The Things Network

Go to [https://www.thethingsnetwork.org](https://www.thethingsnetwork.org)

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/bb43628a-d57b-48da-964f-4ceec09506cb)
Figure 9: The Things Network - Platform

Log in to existing account.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/5910346a-aad2-43a4-9312-e4c5d6365f97)
Figure 10: TheThingsNetwork - Login 1

**NOTE**: Refer to the bottom print label of the gateway, it contains the username & password.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/23ce6810-3265-4506-9659-17289b1a9692)
Figure 11: TheThingsNetwork - Login 2

2. Set up gateway with The Things Network

Click Console.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/4f49e6af-6e76-4ef5-b483-0c8b2d9e13a5)
Figure 12: TheThingsNetwork - Console

Select “au1” for the region.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/625d2e0d-d58f-4fc3-8cb2-2fde0fb7700d)
Figure 13: TheThingsNetwork - Network Cluster

From the console screen, click Gateways.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/292c6f51-0eb4-4e55-8af2-58f229636092)
Figure 14: TheThingsNetwork – Console

Click “Register gateway” for new gateway.  With the provided account, there should be at least one gateway already registered.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/6730ce80-a27c-47a9-823b-80486ced3bc8)
Figure 15: TheThingsNetwork - Gateways

Verify the registered gateway EUI with the EUI on bottom label of the physical gateway.

**NOTE**: LoRaWan gateway must be configured to the same “Gateway Server address”.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/638a48f8-9851-4e6d-8738-7010607ad685)
Figure 16: TheThingsNetwork – Gateway ID

## References
1. [SemTech's LoRa Technology Overview](https://www.semtech.com/lora/what-is-lora)
2. [Building a LoRa-based Device with Arduino](https://www.semtech.com/developer-portal)
3. [CH341 Serial Driver](https://www.wch.cn/downloads/CH341SER_ZIP.html)
