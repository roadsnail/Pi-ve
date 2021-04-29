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

#### Disclaimer - WARNING - If you intend to play along with this project, be very aware that the Hive SLR Boiler Controller will require connecting to a mains electricity supply and that the connections to the controller's Central Heating and Hot Water terminals will be switching at mains voltage! Get it wrong, or touch the wrong parts and serious injury or death may result! You have been warned. If uncertain how to connect the Boiler Controller (SLR2), then obtain advice/assistance from a qualified person.

If you are confident and happy with the warning above and want to make your own Pi-ve, then here is a list of parts:-


* The Hive Active components, the SLT (Thermostat) and SLR2 (Boiler Controller), are easily obtained used from the usual places. The Hive Active hub is not required as this will be replaced by the Raspberry Pi. 
*Although the above picture shows the older thermostat (SLT2). A newer SLT3 may be used instead.*
 
* A Pi Zero W was a freebie when I subscribed to the excellent MagPi magazine. See https://magpi.raspberrypi.org/. Alternatively these are readily available as a kit including case and a USB OTG Host cable.

* A Zigbee USB dongle - I used the ubiquitous CC2531 Zigbee board and programmed it with Koenkk firmware. The picture above shows one of these modules with an antenna enclosed in a USB shell (red) that I had 
in my parts bin.


Next - Add about 1 day to download and configure the software

Result - A standalone Heating/Hot Water Controller, lots of fun, and a chance to learn how to configure a Pi, MQTT broker, Node-RED and Koenkk's Zigbee2MQTT software/firmware

Alternatively buy a Hive Active system and install, but where's the fun and education in that?

---

## The Pi-ve Dashboard - Set up CH/HW On timers and Control your Pi-ve

The below screenshot shows the Pi-ve status/control web page created in node-RED.

It shows the current status of the Pi-ve, online, current time, plus the current temperature/thermostat setting and CH/HW Off/On and 'Demand' states.


![Pi-ve V1 30 Node-RED Dashboard](https://user-images.githubusercontent.com/24318993/116281895-1253c900-a782-11eb-9ccd-9a1f381c17d9.png)
*Example Pi-ve Dashboard screenshot showing Pi-ve 'online', room temperature 19.93 deg C, thermostat setting 21 deg. Heating has been boosted with 29:33 minutes remaining. Looking at the HW Time Slots for the current time (17:41) HW is programmed to 'Off', however 'Override' is active forcing HW On (indicated by the green 'State' LED). Both the CH and HW 'Demand' icons are active (not greyed out)*

* 'Manual' or 'Timer' Setting modes for heating and water.

* Heating and Water Off/On switching.

* Timed On/Off periods for 7 days and up to 8 programmable periods per day (Time Slots) are available for boiler control of heating and hot water.

* An 'Override Timer' function is available allowing the current state of CH or HW to be changed for the duration of a time slot (either off or on).

* Boost functions allow for a 30 minute, 60 minute or 90 minute 'heat on' function for heating and/or water. 
  * Hot water boost will switch on the HW relay for the selected period. 30/60/90 minutes. 'Cancel' will cancel the last boost period selected.
  * Similarly, Heating boost will set the thermostat setting to the current temperature plus 1 deg C for the selected period and 'Cancel will cancel the last boost period.
  
---

## The Pi-ve HTTP Screen - Control Pi-ve with HTTP requests

A screenshot showing Off/On, Manual/Timer Mode and Boost buttons on a simple browser screen that allows for easy control from a smartphone using something like the Android HTTP Request Shortcuts app from Waboodoo - see https://play.google.com/store/apps/details?id=ch.rmy.android.http_shortcuts&hl=en_GB&gl=US 

![Pi-ve-HTTP](https://user-images.githubusercontent.com/24318993/116427789-3ecc1b80-a83c-11eb-9ee8-3b2a4c5422e0.png)

*Example of /ctrl/page showing Pi-ve room temperature 18.94 deg C, thermostat setpoint 20 deg C. Both Heating and Water demand is 'On'  and SLR2 outputs set to demand 'heat' from the attached boiler. 'Timer' is active for water, while 'Boost' is active for a further 59:04 minutes for heating.* 

This allows basic control of the Pi-ve without the 'Time Slot' editing functions provided by the Dashboard screen. It is better optimised for small screen devices.

---

## Control Pi-ve with HTTP request method POST

Pi-ve may be controlled using HTTP JSON formatted requests:-

POST HTTP://ip-address:1880/cmd with Content-Type: application/json

List of valid payloads below. eg. To switch the HW output to off, POST json **{"HW":"Off"}**

### Thermostat setpoint
* {"SP":"22.5"}		*Set Thermostat setpoint to 22.5 degrees C. (Range 1-30, Increments 0.5)*

### Central Heating
* {"CH":"Off"}		*Set CH Switch to Off*
* {"CH":"On"}		*Set CH Switch to On*
* {"CHBoost":"30"}	*Set CH Boost for 30 mins*
* {"CHBoost":"60"}	*Set CH Boost for 60 mins*
* {"CHBoost":"90"}	*Set CH Boost for 90 mins*
* {"CHBoost":"Off"}	*Set CH Boost off*
* {"tmrActive":"CH"} *Set CH Mode to Timer*
* {"manActive":"CH"} *Set CH Mode to Timer*

### Hot Water
* {"HW":"Off"}		*Set HW Switch to Off*
* {"HW":"On"}		*Set HW Switch to On*
* {"HWBoost":"30"}	*Set HW Boost for 30 mins*
* {"HWBoost":"60"}	*Set HW Boost for 60 mins*
* {"HWBoost":"90"}	*Set HW Boost for 90 mins*
* {"HWBoost":"Off"}	*Set HW Boost off*
* {"tmrActive":"HW"} *Set HW Mode to Timer*
* {"manActive":"HW"} *Set HW Mode to Timer*

 

---

## Control Pi-ve by Publishing to Topics on Pi-ve Mosquitto Message Broker

In addition to the above control methods, Pi-ve may be controlled by publishing control payloads to Topics on Pi-ve's Mosquitto Message Broker:-

List of valid payloads below. eg. To set the Thermostat setpoint to **22.5 deg C**, publish to the MQTT message broker at host Pi-ve, topic **pive2mqtt/SLRCtrl/savedSP** payload **22.5**

### Thermostat setpoint
* Topic **pive2mqtt/SLRCtrl/savedSP**	payload **22.5** - *Set Thermostat setpoint to 22.5 degrees C. (Range 1-30, Increments 0.5)*

### Central Heating

* Topic **pive2mqtt/SLRCtrl/CHOffOn**  payload **off** - Switch Heating off
* Topic **pive2mqtt/SLRCtrl/CHOffOn**  payload **heat** - Switch Heating on
* Topic **pive2mqtt/SLRCtrl/CHManAuto**  payload **tmrActiveCH** - Set Timer Mode
* Topic **pive2mqtt/SLRCtrl/CHManAuto**  payload **manActiveCH** - Set Manual Mode

### Central Heating

* Topic **pive2mqtt/SLRCtrl/HWOffOn**  payload **off** - Switch Hot Water off
* Topic **pive2mqtt/SLRCtrl/HWOffOn**  payload **heat** - Switch Hot Water on
* Topic **pive2mqtt/SLRCtrl/HWManAuto**  payload **tmrActiveHW** - Set Timer Mode
* Topic **pive2mqtt/SLRCtrl/HWManAuto**  payload **manActiveHW** - Set Manual Mode



---

## Software/Firmware Sources

Your Pi-ve will require the following software/firmware. Here is a list of sources and instructions for installing the necessary software.

###Firmware
* The CC2531 Zigbee USB Stick - Download and flash it with Koenkk's co-ordinator firmware. I followed the guide at https://www.zigbee2mqtt.io/information/alternative_flashing_methods.html flashing my CC2531 connected to a Raspberry pi.

###Software
* Raspberry Pi OS - https://www.raspberrypi.org/software/operating-systems/ . There are plenty of guides explaining how to install Raspberry Pi OS onto the Pi Zero W so that you may connect in 'headless' mode.

* Mosquitto MQTT Message Broker for Raspberry Pi - Mosquitto and clients can be installed from the repository. In essence, login to your Pi as user Pi, then...

	>sudo apt update
	
	>sudo apt upgrade
	
	>sudo apt-get install mosquitto mosquitto-clients