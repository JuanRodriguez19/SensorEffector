# SensorEffector
CAP1188 8-channel Capacitive Touch (0x2A).

![image of sensor] (https://github.com/JuanRodriguez19/SensorEffector/blob/master/TouchSensor.PNG)

## Table of Contents
1. [Introduction](#introduction)
2. [Budget for Materials Required](#budget-for-materials-required)
3. [Time Schedule](#time-schedule)
4. [Wiring](#wiring)
5. [PCB Design Files](#pcb-design-files)
6. [Assembly for Hardware](#assembly-for-hardware)
7. [PCB Soldering](#pcb-soldering)
8. [Power Up](#power-up)
9. [Testing of Hardware](#testing-of-hardware)
10. [Enterprizing Wifi](#enterprizing-wifi)


### Introduction
The CAP 1188 breakout is a 8-channel capacitive touch sensor. With IC2 communication enabled, the breakout board is able to detect readings from its corresponding pins when they are being touched by users. This project consists of using the Touch Sensor with a Raspberry Pi 3 B+ to detect the readings from the sensor itself and have the lights from each pin illuminate. All information regarding the breakout board can be found [In the Adafruit CAP1188 website](https://learn.adafruit.com/adafruit-cap1188-breakout).

### Budget for Materials Required
The required materials and budget for this project can be found in the documentation folder in this repository or in this link provided.
<a href = "https://github.com/JuanRodriguez19/SensorEffector/blob/master/Documentation/PowerSwitchBudget.pdf">[Budget]</a>

### Time Schedule

### Wiring

You can wire the CAP 1188 Breakout to the Raspberry Pi using the following chart. The AD and RST pins are optional, but in this case the AD pin is mandatory as it is used to achieve the address (0x2A).

| Device Pin                                     | Pi           |
| ---------------------------------------------- | ------------ |
| 1 (GND)                                        | [Ground]     |
| 2 (VIN)                                        | [3.3v]       |
| 3 (SDA)                                        | [BCM 2/SDA]  |
| 4 (SCK)                                        | [BCM 3/SCL]  |
| 5 (RST)                                        | [BCM 17]     |
| 6 (AD) Connected to 3 200k Resistors in Series | [Ground]     |

### PCB Design Files

### Assembly for Hardware

### PCB Soldering

### Power Up

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
