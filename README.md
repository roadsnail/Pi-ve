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
* Zigbee2MQTT from koenkk

---

## Where can I get my very own Pi-ve?

See ingredients above. 

My Hive Active parts, the SLT (Thermostat) and SLR2 (Boiler Controller) was obtained from an Internet auction site. The Hive Active hub is not required  as we will not be controlling this from
a Hive App, but from a device on our own network.

My Pi Zero W was a freeby when subscribing to the excellent Magpie magazine. https://raspberrypipress.imbmsubscriptions.com/the-magpi/

A Zigbee USB dongle. I used the ubiquitous CC2531 board and programmed it with koenkk firmware. The picture above shows on of these modules with an antenna enclosed in a USB shell that I had 
in my parts bin.


Next - Add about 1 day to download and configure the software

Result - A standalone Heating/Hot Water Controller, lots of fun, and a chance to learn how to configure a Pi, MQTT broker, Node-RED and koenkk's Zigbee2MQTT software/firmware

Alternative buy a Hive Active system and install, but where's the fun and education in that?







