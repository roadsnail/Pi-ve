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

## Contents

1. [What is Pi-ve](https://github.com/roadsnail/Pi-ve#what-is-pi-ve)
2. [Where can I get my very own Pi-ve?](https://github.com/roadsnail/Pi-ve#where-can-i-get-my-very-own-pi-ve)
3. [Can I use a Raspberry Pi 3 or 4?](https://github.com/roadsnail/Pi-ve#can-i-use-a-raspberry-pi-3-or-4)
4. [The Pi-ve Dashboard - Set up CH/HW 'On' Timers, 'Boost' and Control your Heating/Hot Water from your Pi-ve](https://github.com/roadsnail/Pi-ve#the-pi-ve-dashboard---set-up-chhw-on-timers-boost-and-control-your-heatinghot-water-from-your-pi-ve)
5. [The Pi-ve HTTP Screen - Control Pi-ve with HTTP requests](https://github.com/roadsnail/Pi-ve#the-pi-ve-http-screen---control-pi-ve-with-http-requests)
6. [Control Pi-ve with HTTP request method POST](https://github.com/roadsnail/Pi-ve#control-pi-ve-with-http-request-method-post)
7. [Control Pi-ve by Publishing to Topics on Pi-ve Mosquitto Message Broker](https://github.com/roadsnail/Pi-ve#control-pi-ve-by-publishing-to-topics-on-pi-ve-mosquitto-message-broker)
8. [Software/Firmware Sources](https://github.com/roadsnail/Pi-ve#softwarefirmware-sources)
9. [Pi-ve software configuration](https://github.com/roadsnail/Pi-ve#pi-ve-software-configuration)

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

#### Disclaimer - WARNING - If you intend to play along with this project, be very aware that the Hive SLR Boiler Controller will require connecting to a mains electricity supply and that the connections to the controller's Central Heating and Hot Water terminals will be switching at mains voltage! Get it wrong, or touch the wrong parts and serious injury or death may result! Also, keep it well away from children and pets whilst developing and testing this. You have been warned. If uncertain how to connect the Boiler Controller (SLR2), then obtain advice/assistance from a qualified person.

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

## Can I use a Raspberry Pi 3 or 4?

Yes, of course. The model 3 and 4 have onboard Wifi making it very suitable for this project. The reason I chose a model Zero W was because it has onboard Wifi and I had one surplus to requirements.
In addition my Pi-ve also runs an additional task of listening to my Bluetooth LE thermometers and relaying temperature data to my Home Automation system. But that's another story...

---

## The Pi-ve Dashboard - Set up CH/HW 'On' Timers, 'Boost' and Control your Heating/Hot Water from your Pi-ve

The below screenshot shows the Pi-ve status/control web page created in node-RED and running on the Pi Zero. Just connect to the node-RED dashboard from a browser on your 
network and browse to URL http://your-pive-ip-address:1880 (inserting your Pi-ve actual IP4 address of course).

It shows the current status of the Pi-ve, online, current time, plus the current temperature/thermostat setting and CH/HW Off/On and 'Demand' states.


![Pi-ve V1 30 Node-RED Dashboard](https://user-images.githubusercontent.com/24318993/116281895-1253c900-a782-11eb-9ccd-9a1f381c17d9.png)
*Example Pi-ve Dashboard screenshot showing Pi-ve 'online', room temperature 19.93 deg C, thermostat setting 21 deg. Heating has been boosted with 29:33 minutes remaining. Looking at the HW Time Slots for the current time (17:41) HW is programmed to 'Off', however 'Override' is active forcing HW On (indicated by the green 'State' LED). Both the CH and HW 'Demand' icons are active (not greyed out)*

* 'Manual' or 'Timer' modes for heating and water.

* Heating and Water Off/On switching.

* Timed On/Off periods for 7 days and up to 8 programmable 'On' periods per day (Time Slots) are available for boiler control of heating and hot water.

* An 'Override Timer' function is available allowing the current state of CH or HW to be changed for the duration of a time slot (either off to on OR on to off).

* A 'Boost' function allow for a 30 minute, 60 minute or 90 minute 'heat on' function for heating and/or water. 
  * Hot water boost will switch on the HW relay for the selected period. 30/60/90 minutes. 'Cancel' will cancel the last boost period selected.
  * Similarly, Heating boost will set the thermostat setting to the current temperature plus 1 deg C for the selected period and 'Cancel' will cancel the last boost period.
  
---

## The Pi-ve HTTP Screen - Control Pi-ve with HTTP requests

A screenshot showing Off/On, Manual/Timer Mode and Boost buttons on a simple browser screen that allows for easy control from a smartphone using something like the Android HTTP Request Shortcuts app from Waboodoo - see https://play.google.com/store/apps/details?id=ch.rmy.android.http_shortcuts&hl=en_GB&gl=US 

![Pi-ve-HTTP](https://user-images.githubusercontent.com/24318993/116427789-3ecc1b80-a83c-11eb-9ee8-3b2a4c5422e0.png)

*Example of /ctrl/page showing Pi-ve room temperature 18.94 deg C, thermostat setpoint 20 deg C. Both Heating and Water demand is 'On'  and SLR2 outputs set to demand 'heat' from the attached boiler. 'Timer' is active for water, while 'Boost' is active for a further 59:04 minutes for heating.* 

This allows basic control of the Pi-ve without the 'Time Slot' editing functions provided by the Node-RED Dashboard screen. Although not offering Time Slot editing functions, it is 
better optimised for small screen devices.

---

## Control Pi-ve with HTTP request method POST

Pi-ve may be controlled using HTTP JSON formatted requests:-

POST HTTP://ip-address:1880/cmd with Content-Type: application/json

List of valid payloads below (in and including the curly brackets). eg. To switch the HW output to off, POST json **{"HW":"Off"}**

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

Your Pi-ve will require the following software/firmware. Here is a list of software sources and brief instructions for installing the necessary software. I suggest installing and configuring the software in the order
below, ensuring that things work properly at each stage of your build.

Some guidance on software configuration is included in the [next section (below).](https://github.com/roadsnail/Pi-ve/blob/main/README.md#pi-ve-software-configuration)

### Firmware
* The CC2531 Zigbee USB Stick - Download and flash it with Koenkk's co-ordinator firmware. I followed the guide at https://www.zigbee2mqtt.io/information/alternative_flashing_methods.html flashing my CC2531 connected to a Raspberry pi.

Other Zigbee USB solutions may be used for this project. I just happened to have a CC2531 surplus to requirements as I have upgraded my main Zigbee network controller to a TI 
CC2652R based module. In my experience, the CC2531 is great at controlling just a few Zigbee devices, but struggles with larger Zigbee networks. In this application, the CC2531 copes 
easily with just two Zigbee connections (the Hive SLR and SLT).

### Software
#### Raspberry Pi OS 
https://www.raspberrypi.org/software/operating-systems/ . There are plenty of guides explaining how to install Raspberry Pi OS onto the Pi Zero W so that you may connect in 'headless' mode.

Following installation of the OS, connect to your Pi and run raspi-config to:-

1. Set a new password for user Pi (mandatory)
2. Set a Hostname for your Pi. I suggest Pive. 
3. Expand Filesystem (optional)


#### Mosquitto MQTT Message Broker for Raspberry Pi
Mosquitto and clients can be installed from the Pi OS repository. In essence, login to your Pi as user Pi, then...
```
sudo apt update
sudo apt upgrade
sudo apt-get install mosquitto mosquitto-clients
```

#### Node-RED
See official install guide here https://nodered.org/docs/getting-started/raspberrypi . Login as user Pi and in home directory run the command on the guide page. This will take some time on the Raspberry Pi Zero.

#### Zigbee2mqtt
Follow the Official installation guide at https://www.zigbee2mqtt.io/getting_started/running_zigbee2mqtt.html AFTER reading the next two tips:-

* Step 2 of the guide - Installing - instructions to 
install Node.js may be omitted as this will have been installed earlier during the node-RED install.

* Also in section 5 of the official guide, the instruction that refers to installation of Zigbee2MQTT on a Pi 1 or Zero and modification of 
ExecStart should be ignored 

Installation of Zigbee2mqtt will take a few minutes, with many warnings thrown up. Don't panic, these may be ignored.

The installation guide should allow the Zigbee2MQTT software to start correctly, however in addition to the configuration settings given in the official guide, please take note 
of the additional configuration notes in the Zigbee2MQTT software configuration section [below.](https://github.com/roadsnail/Pi-ve/blob/main/README.md#pi-ve-software-configuration)

---
## Pi-ve software configuration

* Raspberry Pi OS
Post install configuration discussed above

* Mosquitto MQTT Message Broker for Raspberry Pi

Create Mosquitto Configuration file located at /etc/mosquitto/mosquitto.conf, suggested contents

```
# Place your local configuration in /etc/mosquitto/conf.d/
#
# A full description of the configuration file is at
# /usr/share/doc/mosquitto/examples/mosquitto.conf.example

pid_file /var/run/mosquitto.pid

persistence true
persistence_location /var/lib/mosquitto/

log_dest file /var/log/mosquitto/mosquitto.log

include_dir /etc/mosquitto/conf.d
```



* node-RED

Following installation, set the SYSTEMD to start node-RED at startup thus:
```
pi@pive:~ $ sudo systemctl enable nodered
Created symlink /etc/systemd/system/multi-user.target.wants/nodered.service → /lib/systemd/system/nodered.service.
pi@pive:~ $
pi@pive:~ $ sudo systemctl start nodered
```

Reboot your Pi-ve and ensure node-RED is started by pointing a browser at http://pive-ip-address:1880 and ensure node-RED responds


Next, install some additional node-RED nodes required by the flow listed below. 

These may be installed at the node-RED flow creation screen by selecting 'MENU' - Manage palette

Select the 'Install' tab.

For each of the nodes listed below, enter the name into the 'search' field, then when the node is found and displayed, click 'install'

#### List of additional nodes:-
```
node-red-dashboard
node-red-node-ui-list
node-red-contrib-ui-led
node-red-contrib-ui-media
node-red-contrib-simple-gate
node-red-contrib-moment
```


* Zigbee2mqtt

If you have successfully followed the official Zigbee2MQTT installation notes earlier, your Pi-ve should have started Zigbee and made a connection to the Mosquitto Message broker
running on the Pi.

The following additions should be made to the Zigbee2MQTT configuration.yaml file to:-

* Enable webbased frontend - The webbased frontend to Zigbee2MQTT should be enabled to allow easier setup of the Zigbee connection from the CC2531 co-ordinator to the Hive SLR/SLT devices. 
This can be seen in the example configuration.yaml file below under the section **frontend:** ie set **port:** to **7070** and **host:** to **0.0.0.0**

Documentation for the webbased frontend may be found [here](https://www.zigbee2mqtt.io/information/frontend.html)

* In the **mqtt:** section - Modify the **base_topic:** to be **pive2mqtt** (see below)

* In the **advanced:** section - Set **log_level:** to **error** and **last_seen:** to **epoch** (see example configuration.yaml below)

After making any changes, either reboot your Pi, or restart zigbee2mqtt 
```
sudo systemctl restart zigbee2mqtt
```


Example configuration.yaml
```
homeassistant: false
permit_join: true
mqtt:
  base_topic: pive2mqtt
  server: 'mqtt://localhost'
serial:
  port: /dev/ttyACM0
frontend:
  port: 7070
  host: 0.0.0.0
advanced:
  log_level: error
  last_seen: epoch
  ```

