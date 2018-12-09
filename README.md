# SensorEffector
CAP1188 8-channel Capacitive Touch (0x2A).

![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/TouchSensor.jpg)

## Table of Contents
1. [Introduction](#introduction)
2. [Budget for Materials Required](#budget-for-materials-required)
3. [Time Schedule](#time-schedule)
4. [Assembly of Pi](#assembly-of-pi)
5. [Wiring](#wiring)
6. [PCB Design Files](#pcb-design-files)
7. [PCB Soldering](#pcb-soldering)
8. [Power Up](#power-up)
9.[Case Design](#case-design)
10. [Assembly for Hardware](#assembly-for-hardware)
11. [Testing of Hardware](#testing-of-hardware)
12. [Enterprizing Wifi](#enterprizing-wifi)


### Introduction
The CAP 1188 breakout is a 8-channel capacitive touch sensor. With IC2 communication enabled, the breakout board is able to detect readings from its corresponding pins when they are being touched by users. This project consists of using the Touch Sensor with a Raspberry Pi 3 B+ to detect the readings from the sensor itself and have the lights from each pin illuminate. All information regarding the breakout board can be found [In the Adafruit CAP1188 website](https://learn.adafruit.com/adafruit-cap1188-breakout). Here is a system diagram for the project.
![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/UML.JPG)

### Budget for Materials Required
The required materials and budget for this project can be found in the documentation folder in this repository or in this link provided.
<a href = "https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/PowerSwitchBudget.pdf">[Budget]</a>

### Time Schedule
Realistically, this project should take roughly a weekend to complete if all materials and facilites are available to you. The materials themselves might take a week to arrive due to shipping, but the actual proccess of assembling and programming should not take longer than 3 days. A couple of hours each day can be dedicated towards the different aspects of the project to make time usuage more efficient and effective. For me, this project took around 1 whole semester (4 months) to finish along with an average work time of around 2.5 hours a week. Here is the time schedule I followed: <br>
<br> ![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/TimeCommit.JPG)

### Assembly of Pi
These steps will cover how to set up the Raspberry Pi 3 B+ properly so that you have the ability to log in and test your sensors capabilites.

1. Format an SD card with a minimum of 8GB to be used for the OS of the Pi. You can use the following link to download a SD card formatting software: https://www.sdcard.org/downloads/formatter_4/index.html

2. Download and unzip the latest version of the OS for the Raspberry Pi to your SD card. Download NOOBS in the link as that will ensure that you will have almost everything required when starting: https://www.raspberrypi.org/downloads/noobs/   

3. Once the image is on the SD card, remove it from the pc and insert it in the Pi. Now plug in a seperate monitor, mouse, keyboard, HDMI, ethernet cable, and power supply to the Pi in their corresponding ports. The Pi turns on automatically when the power is plugged in.

4. Upon the boot up session, select Raspbian as the operating system for the Pi and follow the instructions as they appear. You may also change the keyboard layout on the bottom during intial boot. The US layout is highly reccommended.

5. Once installation is completed, you should be brought to the desktop. Connect yourself to either Wifi or wired connection in order to perform the next few steps.

6. Open the terminal in the top left corner of the screen and input the following lines (this takes quite a long time):
	```Shell
	wget https://raw.githubusercontent.com/six0four/StudentSenseHat/master/firmware/hshcribv01.sh \  
	-O /home/pi/hshcribv01.sh  
	chmod u+x /home/pi/hshcribv01.sh  
	/home/pi/hshcribv01.sh  
	```

7. Now it is time to set up a VNC connection so that you can access your Pi on any computer screen. From the Start Menu, go -> Preferences->Raspberry Pi Configuration->Interfaces, then set VNC to Enabled. Now on the destop in the top right corner, you should see a VNC logo. When you click it you should see an IP address for your Pi which will be used to connect it via the VNC software. Download the software on any computer you wish to communicate with the Pi: https://www.realvnc.com/en/connect/download/vnc/

8. Once the software is installed, connect the ethernet cable from the Pi to your computer of choice to have a direct connection. Now you can simply input the same address you found in the Pi in the VNC software and it should connect.

9. To turn off the Pi, type `sudo powerdown` in the terminal. 

If you are still unsure or struggling with a part in particular, this video provides a step by step explanation for everthinf required: https://www.youtube.com/watch?v=xBlxuf_LSCM


### Wiring
Before wiring the sensor to the breadboard, it is important to solder the pins that come included to the sensors corresponding pin layouts. Addtionally, make sure to cut 3 pins off each set of pin rows as those are extra pins not required. 
![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/SensorPins.JPG)

When soldering, make sure you have safetly glasses equipped along with having proper ventilation that contains a extractor arm for the fumes. A soldering toolkit is also required which is available in most labs.
Here is a great soldering tutorial to help with those unsure.<br>
https://www.youtube.com/watch?v=3230nCz3XQA

The Sensor should now look like this:<br>

Bottom View <br>
![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/SolderingSens.JPG) <br>

Top View <br>
![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/SolderingSens2.JPG) <br>

You can wire the CAP 1188 Breakout to the Raspberry Pi using the following chart. The AD and RST pins are optional, but in this case the AD pin is mandatory as it is used to achieve the address (0x2A).

| Device Pin                                     | Pi           |
| ---------------------------------------------- | ------------ |
| 1 (GND)                                        | [Ground]     |
| 2 (VIN)                                        | [3.3v]       |
| 3 (SDA)                                        | [BCM 2/SDA]  |
| 4 (SCK)                                        | [BCM 3/SCL]  |
| 5 (RST)                                        | [BCM 17]     |
| 6 (AD) Connected to 3 200k Resistors in Series | [Ground]     |



This is the layout for the pins of the Raspberry pi<br>

![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/Pinouts.JPG)


This is how it would look connected to the pi.
![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/BreadBoardWiring.jpg)


This would be with the 3 200k resistors connected to pin AD
![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/IMG_0882.jpg)


### PCB Design Files
In order to develop the PCB design files, the appilcation Fritzing is required along with the CAP 1188 Sensor file which must be added to the application. The file can be downloaded <a href = "https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/Adafruit%20CAP1188%20-%208-Key%20Capacitive%20Touch%20Sensor%20Breakout%20(1).fzpz">Here</a>

Once the Sensor is added to parts, you can create a frizting diagram for the wiring of the pi and sensor. It should look similar to this.
![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/TouchSensor_bb.png)

From here you can create the PCB design from the wiring you just designed. The PCB layout should look similar to this.

![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/TouchSensor_pcb.png)

With these now ready, you can put together your Gerber files and create your PCB using a lazer cutter machine.
The Gerber files are located and can be downloaded <a href = "https://github.com/JuanRodriguez19/SensorEffector/tree/master/Gerber">Here</a>

### PCB Soldering
Using the same rules as when soldering the Sensor, solder pieces of wire in between the 6 vias on the PCB board. Once thats done, solder the 20 pin socket to the PCB board to the corresonding holes for where the pi would connect. For the other 2 20 pin sockets you have, remove 4 pins from each side with a pair of tweezers so that it can match up with the holes in the sensors location. Lastly solder the 3 resistors in their correct locations according to your PCB design files. Your final board should look similar to this.

Top view with sensor connected: <br>
![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/IMG_0924.jpg)

Bottom view: <br>
![imageofsensor](https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/PcbBottom.JPG)

### Power Up

### Case Design 

### Assembly for Hardware

### Testing of Hardware

### Enterprizing Wifi

Connecting to Enterprise Wi-Fi can be a challenge but the graphical desktop has come a long way from where it was, please share your respective successes in situations where the GUIs do not work - here is my configuration:

1.  In /etc/network/interfaces:
	```
	auto lo
	iface lo inet loopback
	iface eth0 inet dhcp
	allow-hotplug wlan0
	iface wlan0 inet manual
	wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
	iface default inet dhcp
	```

2.  In /etc/wpa_supplicant/wpa_supplicant.conf:
	```
	ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
	update_config=1
	network={
        ssid="myWi-Fi@Humber"
        proto=RSN
        key_mgmt=WPA-EAP
        pairwise=CCMP
        auth_alg=OPEN
        eap=PEAP
        identity="n12345678"
        password="aaaAAA12"
        phase2="auth=MSCHAPV2"
	}
	```

	I have been told that more recently the Prototype Lab staff have said to use:
	```
	sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
	```

	Add the follow to file and fill in identity and password field save and restart RPI:
	```
	network={
	ssid="myWi-Fi@Humber"
	priority=999
	proto=RSN
	key_mgmt=WPA-EAP
	pairwise=CCMP
	auth_alg=OPEN
	eap=PEAP
	identity="STUDENT ID"
	password="PASSWORD"
	phase1="peaplabel=0"
	phase2="auth=MSCHAPV2"
	}
	```
	Even more recently the Prototype Lab staff have successfully tested the 
	following sample configuration file. The configuration includes sections 
	for Humber’s myWi-fi, Eduroam, home WPA encrypted networks, and open networks like “Welcome To Humber”.:
	```
	# Sample configuration file for Raspberry Pi to connect to various WiFi networks.
	# /etc/wpa_supplicant/wpa_supplicant.conf

	ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
	update_config=1
	country=CA

	# sample network configuration for Humber College myWi-Fi
	# change text in <> to your account values (remove the < and > while doing this )
	network={
		ssid="myWi-Fi@Humber"
		key_mgmt=WPA-EAP
		auth_alg=OPEN
		eap=PEAP
		identity="<YourHCNetID>"
		password="<YourHCnetPassword>"
		phase1="peaplabel=0"
		phase2="auth=MSCHAPV2"
		priority=999
		proactive_key_caching=1
	}

	# Sample network configuration for joining Eduroam Wi-Fi network
	# change text in <> to your account values (remove the < and > while doing this )
	network={
		ssid="eduroam"
		scan_ssid=1
		key_mgmt=WPA-EAP
		eap=PEAP
		identity="<YourHCnetID>@humber.ca"
		password="<YourHCnetPassword>"
		phase1="peaplabel=0"
		phase2="auth=MSCHAPV2"
		proactive_key_caching=1

	}

	# Sample network configuration for joining a home wi-fi network.
	# change text in <> to your network values (remove the < and > while doing this )
	network={
		ssid="<yourNetworkSSID"
		psk="<yourNetworkPassword>"
		proto=RSN
		key_mgmt=WPA-PSK
		pairwise=CCMP
		auth_alg=OPEN
	}

	#Sample networtk configuration for joining open, unsecured network
	network={
		ssid="<yourNetworkSSID>"
		key_mgmt=NONE
	}
	```
	
3.  Download Humber Certificate (For HumberSecure).cer from https://its.humber.ca/wireless/humbersecure/

4.  Reboot
