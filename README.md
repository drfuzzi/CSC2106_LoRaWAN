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

1. **OLED Display Integration**
   - Display the following information on the OLED for both LoRa Receiver & Sender:
     - "Setup Successful"
     - "Setup Failed"
     - "Sending Message"
     - "Waiting for Reply"
     - “Message Received”
   - Refer to [`ssd1306_i2c.ino`](ssd1306_i2c.ino) for OLED display implementation. Install the “Adafruit SSD1306” library first.

2. **Enhance Peer-to-Peer Reliability**
   - Implement features to prevent crosstalk traffic interference, e.g., ACK and retransmit.

3. **Improve Message Protocol**
   - Develop ID-based messaging with a header, payload, and checksum supporting at least three devices, i.e. simple message filtering, only accepting messages that are directed to the node's agreed ID.

## References
1. [SemTech's LoRa Technology Overview](https://www.semtech.com/lora/what-is-lora)
2. [Building a LoRa-based Device with Arduino](https://www.semtech.com/developer-portal)
3. [CH341 Serial Driver](https://www.wch.cn/downloads/CH341SER_ZIP.html)
