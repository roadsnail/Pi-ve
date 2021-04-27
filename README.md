# Pi-ve
Raspberry Pi Zero W controls a Hive SLR/SLT - A standalone Heating/Hot water control solution (without the British Gas 'Cloud').

Control your Central Heating/Hot Water boiler on your local network using Pi-ve controlled from:-

* Node-RED Dashboard (in a Web browser)
* HTTP Requests
* Messages published to an onboard MQTT message broker

![Pi-ve_1](https://user-images.githubusercontent.com/24318993/116269807-6c4e9180-a776-11eb-95e4-f6336ae7906d.png)

---

## What is Pi-ve?

### Pi-ve =

Hardware: 
* 1 off Raspberry Pi Zero W + PSU +
* 1 off Zigbee USB Controller (eg. CC2531) + 
* British Gas Hive Active Heating Thermostat/Boiler Controller (SLR/SLT)  (Minus Hive Active Hub)

Software:
* Raspberry Pi OS (Buster Lite)
* MQTT Broker - Mosquitto
* Node-RED
* Zigbee2MQTT from Koenkk - see https://github.com/Koenkk/zigbee2mqtt

---

## Where can I get my very own Pi-ve?

#### Firstly - WARNING - If you intend to play along with this project, be very aware that the Hive SLR Boiler Controller will require connecting to a mains electricity supply and that the connections to the controller's Central Heating and Hot Water terminals will be switching at mains voltage! Get it wrong, or touch the wrong parts and serious injury or death will  result! You have been warned. If uncertain how to connect the Boiler Controller, then get advice from a qualified person.

So, moving on...

See Hardware ingredients above. 

* The Hive Active components, the SLT (Thermostat) and SLR2 (Boiler Controller), were obtained from an Internet auction site. A Hive Active hub is not required as we will not be controlling this from
a Hive App, but from a device on our own network. Although the above picture shows the Hive Active Boiler Controller SLR2 (Dual Central Heating/Hot Water) and the older thermostat (SLT2). A newer SLT3 may be used.
 
* A Pi Zero W was a freeby when subscribing to the excellent Magpie magazine. See https://raspberrypipress.imbmsubscriptions.com/the-magpi/. Alternatively these are readily available as a kit including case and micro-USB to USB cable

* A Zigbee USB dongle - I used the ubiquitous CC2531 Zigbee board and programmed it with Koenkk firmware. The picture above shows one of these modules with an antenna enclosed in a USB shell (red) that I had 
in my parts bin.


Next - Add about 1 day to download and configure the software

Result - A standalone Heating/Hot Water Controller, lots of fun, and a chance to learn how to configure a Pi, MQTT broker, Node-RED and koenkk's Zigbee2MQTT software/firmware

Alternatively buy a Hive Active system and install, but where's the fun and education in that?

---
![Pi-ve V1 30 Node-RED Dashboard](https://user-images.githubusercontent.com/24318993/116281895-1253c900-a782-11eb-9ccd-9a1f381c17d9.png)







