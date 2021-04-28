# Pi-ve
A Raspberry Pi Zero W controls a Hive Active Thermostat (SLTx) /Boiler Controller (SLR2) - A standalone Central Heating (CH)/ Hot Water (HW) control solution (without the British Gas 'Cloud').

Control your Central Heating/Hot Water boiler on your local network using Pi-ve controlled from:-

* Node-RED Dashboard (in a Web browser)
* HTTP Requests
* Messages published to an onboard MQTT message broker

The Node-RED dashboard Web page offers full control of CH and HW with up to 8 programmable 'On' periods per day plus Override/Boost functions.

In addition, the Pi-ve may be controlled using MQTT commands OR HTTP Requests from an external system (eg. A Home Automation platform).

![Pi-ve_1](https://user-images.githubusercontent.com/24318993/116269807-6c4e9180-a776-11eb-95e4-f6336ae7906d.png)

*Pi-ve System - SLR2, Zigbee USB Stick (attached to Raspberry Pi Zero W), SLT2*

---

## What is Pi-ve?

### Pi-ve =

Hardware: 
* 1 off Raspberry Pi Zero W (kit inc. Case and micro-USB cable) + PSU + micro SD card 
* 1 off Zigbee USB Controller (eg. CC2531) + USB Housing +
* British Gas Hive Active Heating Thermostat/Boiler Controller (SLR2/SLT2) or (SLR2/SLT3). The Hive Active Hub is NOT required.

Software:
* Raspberry Pi OS (Buster Lite)
* MQTT Broker - Mosquitto
* Node-RED
* Zigbee2MQTT from Koenkk - see https://github.com/Koenkk/zigbee2mqtt

Firmware:
* Koenkk firmware for the CC2531 - see https://www.zigbee2mqtt.io/information/flashing_the_cc2531.html

---

## Where can I get my very own Pi-ve?

#### Firstly - Disclaimer - WARNING - If you intend to play along with this project, be very aware that the Hive SLR Boiler Controller will require connecting to a mains electricity supply and that the connections to the controller's Central Heating and Hot Water terminals will be switching at mains voltage! Get it wrong, or touch the wrong parts and serious injury or death may result! You have been warned. If uncertain how to connect the Boiler Controller (SLR2), then obtain advice/assistance from a qualified person.

If you are confident and happy with the warning above and want to make your own Pi-ve, then here is a list of parts:-


* The Hive Active components, the SLT (Thermostat) and SLR2 (Boiler Controller), were obtained from an Internet auction site. A Hive Active hub is not required as we will not be controlling this from
a Hive App, but from a device on our own network. The Raspberry Pi Zero W. 
*Although the above picture shows the older thermostat (SLT2). A newer SLT3 may be used.*
 
* A Pi Zero W was a freebie when I subscribed to the excellent MagPi magazine. See https://magpi.raspberrypi.org/. Alternatively these are readily available as a kit including case and micro-USB to USB cable

* A Zigbee USB dongle - I used the ubiquitous CC2531 Zigbee board and programmed it with Koenkk firmware. The picture above shows one of these modules with an antenna enclosed in a USB shell (red) that I had 
in my parts bin.


Next - Add about 1 day to download and configure the software

Result - A standalone Heating/Hot Water Controller, lots of fun, and a chance to learn how to configure a Pi, MQTT broker, Node-RED and Koenkk's Zigbee2MQTT software/firmware

Alternatively buy a Hive Active system and install, but where's the fun and education in that?

---

## Pi-ve Dashboard - Set up CH/HW On timers and Control your Pi-ve

The below screenshot shows the Pi-ve status/control web page created in node-RED.

It shows the current status of the Pi-ve, online, current time, plus the current temperature/thermostat setting and CH/HW states.


![Pi-ve V1 30 Node-RED Dashboard](https://user-images.githubusercontent.com/24318993/116281895-1253c900-a782-11eb-9ccd-9a1f381c17d9.png)

* Manual or Timer Setting modes for heating and water.

* Heating and water Off/On switching.

* Timed On/Off periods for 7 days and up to 8 programmable periods per day (Time Slots) are available for boiler control of heating and hot water.

* An 'Override Timer' function is available allowing the current state of CH or HW to be changed for the duration of a time slot (either off or on).

* Boost functions allow for a 30 minute, 60 minute or 90 minute 'heat on' function for heating and/or water.









