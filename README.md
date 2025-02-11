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
<br />*Figure 1: LoRa-RFM + UNO (End Device)*

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/9e3b5763-1795-40fc-8bb3-373d845d4ce7)
<br />*Figure 2: WisGate Edge Lite (Gateway)*

In short, LoRaWAN is an example of a low power wide area network that is based on LoRa radio modulation. While Semtech provides the LoRa radio chips, the LoRa Alliance, drives the standardization and harmonization of the LoRaWAN protocol. 

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/1055b93c-431e-4b13-a4f0-486cd3d9a21d)
<br />*Figure 3: LoRaWAN Architecture*

The architecture of a LoRaWAN network is shown above. 

-	End devices (nodes): Transmit their payloads in what is known as an uplink message, to be picked up by a LoRaWAN gateway. A key aspect of LoRaWAN is that a device is not associated with a single gateway and its payloads may be picked up by any number of LoRaWAN gateways within the device’s range. 
- Gateway: Pass messages to its associated LoRaWAN network server (LNS), usually carried out over Wi-Fi or Ethernet. Cellular and satellite gateways are available to enable very remote solutions without relying on an internet connection. There are various options for network servers, for example The Things Network (TTN). The LNS receives the messages from the gateway and checks whether the device is registered on its network; the LNS also carries out decoupling, since the message may be received and uploaded by multiple gateways. The message is then forwarded to the application server on which the device is registered. 

Communication is also possible in the other direction, where a message is sent as a downlink to the node. The downlink message is sent from the application server to the network server. The network server then queues the downlink, and when the device next sends an uplink message, the network server will pass the downlink message to the nearest gateway which received the uplink. The gateway then broadcasts the downlink message for the device to receive. Common uses for a downlink message are to update a device’s broadcast settings (i.e. updates more/less frequent) or trigger some other action (e.g. causing a device to open/close or turning the power on/off).



## Lab Exercise

In this exercise, we will use the LoRa-RFM + UNO as the end device communicating to the WisGate Edge Lite as the gateway. And subsequently, via the IP network, platform such as TheThingsNetwork acts as the network server to manage the gateways, end-devices, applications. It also acts as the Application Server processing application-specific data messages received from end devices.
Ensure that the Maker UNO is connected to the Cytron LoRa-RFM Shield, as shown below.

### 1. Gateway Setup (for reference, skip for in-lab exercise)
**1.1 Attach the LoRa Antenna**

First and foremost, screw on the antenna to the RP-SMA connector on the back panel of the RAK7268/C WisGate Edge Lite 2.

**WARNING**: Do not power the device if the LoRa Antenna port has been left open to avoid potential damage to the RAK7268/RAK7268C WisGate Edge Lite 2.

**1.2 Power the gateway ON**

It is recommended to use the 12 V DC adapter that comes with the RAK7268/RAK7268C WisGate Edge Lite 2. Optionally, you can use your own PoE cable and injector since the device supports PoE.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/856cd97c-a247-4530-998b-b41902288c32)
<br />*Figure 4a: RAK7268/C WisGte Edge Lite 2 Top View*            

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/11a64b0d-ec89-45de-b887-aa6e29d6bb70)
<br />*Figure 4b: RAK7268/C WisGate Edge Lite 2 Back Panel*


### 2. Gateway Configuration (for reference, skip for in-lab exercise)

**2.1 Access the Gateway**

In this section, several ways of accessing the gateway are provided to have different alternatives for you to choose from depending on the availability of the requirements needed.

**WARNING**: Do not power the device if the LoRa Antenna port has been left open to avoid potential damage to the RAK7268/RAK7268C WisGate Edge Lite 2.

**2.1.1 Wi-Fi AP Mode**

By default, the gateway will work in Wi-Fi AP Mode which means that you can find an SSID named RAK7268_XXXX on your PC’s Wi-Fi Network List. XXXX is the last two bytes of the gateway’s MAC address.

No password is required to connect via Wi-Fi
Using your preferred Web browser, log in with the credentials provided below:

-	Browser Address: 192.168.230.1
-	Username: root
-	Password: admin12345678!

**NOTE**: Please do not change the password. 

**2.1.2 WAN Port (Ethernet)**

Connect the Ethernet cable to the port marked ETH on the gateway and the other end to the PoE port of the PoE injector. Connect the LAN port of the PoE injector to your PC. The default IP is 169.254.X.X. The last two segments (X.X) are mapped from the last four bits of the MAC address of your gateway. For example, the last four bits of the MAC address are 0F:01, and the IP address is 169.254.15.1. Make sure to manually set the address of your PC to one in the same network (for example 169.254.15.100). Use the same credentials for the Web UI as for AP mode. (MAC address is also indicated as the GWEUI, on the gateway bottom print label)

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/2f2cfbc9-707d-43ae-8fdf-d0f1976de236)
<br />*Figure 5: Wisgate - Web UI Login Page*

**2.2 Access the Internet**

**Connect through Wi-Fi**

Go into the Network>Wi-Fi->Settings 

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/e06226e9-eb62-45cd-9bae-e8cc46f0abd8)
<br />*Figure 6: Wisgate- WiFi Menu Page*

Select DHCP Client in the Mode field. Enter or click “Scan” to choose your ESSID, select the right Encryption method and enter the correct Key.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/7da5bf31-818e-406f-ab25-23e2f2b8bdc2)
<br />*Figure 7: Wisgate - Connect through Wi-Fi Credentials*

**NOTE**: Assuming you have entered the correct parameter values you should get an IP address assigned by your Wi-Fi router’s (AP) built-in DHCP server. You can use this new IP address to log in via a web browser (same way as in AP mode).

**2.3 Setup Gateway with TTN Credentials**

-	Select Work mode as “Packet forwarder”.
-	Enter Server URL as “au1.cloud.thethings.network”.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/dae28949-6f4d-4952-8603-0fd4a73bd18d)
<br />*Figure 8: Wisgate – Packet Forwarder Mode*

### 3. Gateway Configuration with The Things Network (for reference, skip for in-lab exercise)

**3.1 Set up account with The Things Network**

Go to [https://www.thethingsnetwork.org](https://www.thethingsnetwork.org)

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/bb43628a-d57b-48da-964f-4ceec09506cb)
<br />*Figure 9: The Things Network - Platform*

Log in to existing account.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/5910346a-aad2-43a4-9312-e4c5d6365f97)
<br />*Figure 10: TheThingsNetwork - Login 1*

**NOTE**: Refer to the bottom print label of the gateway, it contains the username & password.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/23ce6810-3265-4506-9659-17289b1a9692)
<br />*Figure 11: TheThingsNetwork - Login 2*

**3.2 Set up gateway with The Things Network**

Click Console.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/4f49e6af-6e76-4ef5-b483-0c8b2d9e13a5)
<br />*Figure 12: TheThingsNetwork - Console*

Select “au1” for the region.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/625d2e0d-d58f-4fc3-8cb2-2fde0fb7700d)
<br />*Figure 13: TheThingsNetwork - Network Cluster*

From the console screen, click Gateways.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/292c6f51-0eb4-4e55-8af2-58f229636092)
<br />*Figure 14: TheThingsNetwork – Console*

Click “Register gateway” for new gateway.  With the provided account, there should be at least one gateway already registered.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/6730ce80-a27c-47a9-823b-80486ced3bc8)
<br />*Figure 15: TheThingsNetwork - Gateways*

Verify the registered gateway EUI with the EUI on bottom label of the physical gateway.

**NOTE**: LoRaWan gateway must be configured to the same “Gateway Server address”.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/638a48f8-9851-4e6d-8738-7010607ad685)
<br />*Figure 16: TheThingsNetwork – Gateway ID*

Frequency Plan: “AU_915_928_FSB_2”.
May selected a different frequency plan via “General Settings”.

**NOTE**: Frequency plan selection is dependent on the operating frequency of the LoRaWAN gateway.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/26a837f8-5573-4069-84c5-c6d380f8ae37)
<br />*Figure 17: TheThingsNetwork – Frequency Plan*

Once the gateway is registered, and if the gateway is communicating to The Things network, the status should display as connected.

### 4. Application Configuration with The Things Network (for reference, skip for in-lab exercise)

Click “Create application” for new application.  

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/1bd6b52d-7d40-4d10-8161-e81c7658e2f3)
<br />*Figure 18: TheThingsNetwork – Applications*

The application ID should be in lower case and used to uniquely identify your application on the network.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/1ed0729a-66d9-45d0-98cc-b866c6583c59)
<br />*Figure 19: TheThingsNetwork – Applications ID*

###	5. Register End-Device with The Things Network (for reference, skip for in-lab exercise)

On the Application tab, Click “Register end device”.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/e0fc3d17-8023-4c03-88e0-5e3130d5baeb)

-	Frequency Plan: “Australia 915-928 MHz, FSB 2”
-	LoRaWan Version: “LoRaWan Specification 1.0.2”
-	Regional Parameters Version: “RP001 Regional Parameters 1.0.2 revision B”
-	Activation mode: Over The Air Activation (OTAA)
-	Additional LoRaWAN class capabilities: None (Class A only)

**NOTE**: Because the MCCI LoRaWAN LMIC Library has only been tested with LoRaWAN 1.0.2/1.0.3 networks.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/307f8efc-3b39-45f3-9edf-a8a970df31d2)
<br />*Figure 20: TheThingsNetwork – Register End Device 1*

-	Choose and enter End Device ID.
-	Join EUI: 00 00 00 00 00 00 00 00
-	Application EUI: Auto-generate.
-	App Key: Auto-generate.

Take note of the Application/Join EUI, Device EUI and the App Key. These keys are needed later to set up the LoRa-RFM + UNO.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/ef026426-3284-4048-96b4-bb034a6537b7)
<br />*Figure 21: TheThingsNetwork – Register End Device 2*

Choose and enter a Device ID and an eight-byte Device EUI.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/0fbf9e65-0dbb-408e-96ce-a615d19491d6)
<br />*Figure 22: TheThingsNetwork – Register End Device 3*

###	6. End Device Configuration 

**6.1 LoRaWAN Library Install**

-	Install the MCCI LoRaWAN LMIC library.
-	In the Arduino IDE, select menu Sketch | Include Library | Manage Libraries
-	In the search box enter: MCCI
-	Click the MCCI LoRaWAN LMIC library by Terry Moore.
-	Select the latest version and press the Install button.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/ebc852a5-5b15-4883-84ff-d549c8ee7acf)

**6.1.1 Configure the MCCI LoRaWAN LMIC Library**
- Edit file lmic_project_config.h.
- This file can be found at: ".../libraries/MCCI_LoRaWAN_LMIC_library/project_config"
- Comment "#define CFG_us915 1", uncomment "#define CFG_au915 1"
  
![project_config](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108822683/c3148703-6372-4ebf-969c-f5b4f2455455)

**6.2 End Device LoRaWAN Configuration**

The LoRa-RFM transceiver module does not have a built-in DevEUI or AppEUI. In such a case you should let the TTN console generate the required DevEUI or AppEUI. Here below is an example of generated AppEUI, DevEUI, and AppKey in the TTN console.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/22803439-5888-47ad-a802-d7a52b4c664f)

**NOTE**: AppEUI, DevEUI, and AppKey are used in the Arduino sketch. In this Arduino sketch, the DevEUI or AppEUI must be converted to an array of 16 bytes in LSB order.  The AppKey must be converted to an array of 32 bytes in MSB order. I have found an online tool that converts these values to a bytes array in its correct order (LSB/MSB). Kindly use this online tool to prevent any negligence.

https://www.mobilefish.com/download/lora/eui_key_converter.html

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/8298a646-9030-4155-9736-9f951ab49b93)

Open Arduino IDE. Copy and paste the code from link below. You need to do some adjustments to the code later.

https://gist.githubusercontent.com/NorHairil/af7e959d92c249724db69cee6074f387/raw/6d4dc22ed6c4303cff84b6a654d8b8fc69c76aa6/DHT22node.ino

From the online tool, copy DevEUI, AppEUI, and AppKey that you had converted and paste them into the sketch.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/48ae9c5a-6a1b-4b06-8f3e-7e1e1044939f)

For this part, you can double-check by checking on the shield board itself to find the correct pin mapping. This is the pin mapping for the Cytron Shield-LoRa-RFM board.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/cdcb9458-49ca-43ad-ac44-75736b566985)

**6.3 Compile and Upload the Code**

Connect the Arduino board to your computer using the USB cable.
In the Arduino IDE, select menu Tools > Board and select Arduino Uno. Then, select menu Tools > Port: your port.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/3eea14ae-cb3f-4171-89fb-5c9dc5ef7af4)

Compile ttsce-otaa-helloworld sketch. You should not see any errors (but there are warnings).

Upload the ttsce-otaa-helloworld sketch to the Arduino board. You should not see any errors.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/32b58143-f404-428f-970e-5b7fa8e4ad5d)

You can open the Serial Monitor to check if your node is successfully connected to The Things Stack. In a few seconds, the Serial Monitor will show your NWSKEY and APPSKEY of your node if you have successfully connected to The Things Network.

**6.4 Display Data on The Things Network**

In the sample code, ”helloworld” message is transmitted every 60 seconds.

If you want to convert the payload into readable text:

-	Select your end device in the “End devices Overview” screen.
-	Select “Payload formatters”.
-	Select “Uplink”.
-	Select “Formatter type: Javascript”.

![image](https://github.com/drfuzzi/CSC2106_LoRaWAN/assets/108112390/34ecdb01-bab4-4060-8a75-75886f0f52e7)

Finally, if both your node and gateway functioning well, you should see the number of sent uplinks and received downlinks.

## References
1. [SemTech's LoRa Technology Overview](https://www.semtech.com/lora/what-is-lora)
2. [Building a LoRa-based Device with Arduino](https://www.semtech.com/developer-portal)
3. [CH341 Serial Driver](https://www.wch.cn/downloads/CH341SER_ZIP.html)
4. [RAK7268 WisGate Edge Lite 2 User Guide](https://manuals.plus/rak/rak7268-wisgate-edge-lite-2-8-channel-indoor-lorawan-gateway-manual#axzz8RboGw8VH)
5. [Cytron LoRa-RFM Shield + Arduino UNO User Guide](https://sg.cytron.io/tutorial/displaying-dht22-sensor-data-at-thingspeak-with-lorawan-network)
6. [WisGateOS 2 Basics Station to TTNv3](https://docs.rakwireless.com/Product-Categories/WisGate/RAK7268-V2/Supported-LoRa-Network-Servers/#wisgateos-2-basics-station-to-ttnv3)
