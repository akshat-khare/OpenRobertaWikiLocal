<p align="center"><em>It is highly recommended to checkout the raspberry's websites, especially <a href="https://www.raspberrypi.org/help/">https://www.raspberrypi.org/help/</a>, where you will find all information about the necessary steps to get started.</em></p>

## First time setup for System and WiFi router

In addition to your Raspberry Pi 2 and a [micro SD card] (https://www.raspberrypi.org/documentation/installation/sd-cards.md) for the system you will need:
* micro USB-cable (power cable)
* ethernet cable
* USB wifi adaper
* USB keyboard and mouse (see headless installation)
* monitor with HDMI cable (see headless installation)

you can get more information [here](https://www.raspberrypi.org/documentation/setup/)

### Preparing the SD-Card
The README site from Raspberry Pi 2 provides you all necessary information to download, extract and install the image to an SD card: [Installing Operating System Images](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)

There are 3 possibilities to get a raspian image
* NOOBS easy installer for Raspbian (and others). Use this, if you have no keyboard/mouse or monitor available -> see headless installation
* NOOBS Lite network installer for Raspbian (and others)
* RASPBIAN  
 
We have tried all of them, they work without any issues.

#### Headless Installation
If you don't have a monitor and/or mouse and keyboard on hand, download [NOOBS easy install for Rasbian](https://downloads.raspberrypi.org/NOOBS_latest), unzip and copy the image to the SD card and open the file `recovery.cmdline` with a simple editor.

Add ` silentinstall` at the end of the first (and only) line, so that it looks like this   
`runinstaller quiet ramdisk_size=32768 root=/dev/ram0 init=/init vt.cur_default=1 elevator=deadline silentinstall` [(Paul Lunow)](http://www.interaktionsdesigner.de/2014/raspberry-pi-ohne-monitor-tastatur-und-maus-in-betrieb-nehmen/)

Plug in the network and power cable. After the first boot (ca. 30 min, only the red LED is on) your Raspberry Pi will be visible in your routers DHCP table as raspberry. You can now easily log in to your raspberry via ssh from any computer/laptop in your local network.



### Configuring the Raspberry Pi 

Now slot in the SD card into your Raspberry Pi 2, connect a USB-Keyboard and Ethernet cable as well as a monitor and finally your micro usb power supply. Your Raspberry Pi 2 will turn on and boot from the SD card. Now login or connect to your Raspberry Pi via ssh (headless only) and login.

Default login information is:
```
User: pi
Password: raspberry
```

It is a good idea to configure the Raspberry Pi to your needs. The first basic configuration can be done via the Raspberry Pi configuration  tool, for detailed information have a look [here](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).

####  Raspberry Pi Configuration
Open a terminal or log in via ssh.  
`$ sudo raspi-config` starts the configuration tool.     
You can easily jump between the menu items with the up and down arrow keys. To select, finish or ok press the right or levt arrow keys or use the Tab key.
 
1. Expand Filesystem, to make sure there is enough space on your SD card (NOOPS users' file system is expanded automatically during installation).
1. Change User Password, if you want to (recommended). The username will still be pi.
1. Boot Options, nothing to do.
1. Wait for Network at Boot, nothing to do.
1. Internationalisation Options, recommended (NOOPS Lite seems to have the correct settings).
  1. Change Locale, set up language and regional settings, for Germany e.g. choose "de_DE.UTF-8 UTF-8" (type Space to get a star there).
  1. Change Timezone, set up timezone to match your location.    
  1. Change Keyboard Layout, set the keyboard layout to match to your own, for Querz find a generic keyboard with 105 keys and choose German.
1. Enable Camera, nothing to do.
1. Add to Rastrack, why not?
1. Overclock. Set to “medium” if you go any further you will need cooling for the raspberry pi.
1. Advanced Options 
  1. Memory Split. Set to 16.

Back at the raspi-config home screen click “finish” (2x Tab).  
Reboot your Raspberry Pi with `$ sudo reboot`.

#### Update the System
After the reboot make sure your Raspberry Pi is up-to-date. You will require internet connection for this!   
`$ sudo apt-get update` update the list of available packages  
`$ sudo apt-get upgrade` update the packages   
`$ sudo reboot`  

## Wifi Access Point
Configuring the Raspberry Pi as an wireless access point is very helpful for our purposes. At the end you will have an all-in-one device as a classroom setup to program robots with the Open Roberta Lab. If you have a wireless router on hand and would like to use it you can skip this step.

Configuring the Raspberry Pi as a wireless access point and router takes some time. Please check out the instructions and explanations on http://jankarres.de/2015/06/raspberry-pi-wlan-access-point-einrichten/. They are great and work with
* Edimax EW-7811Un 150Mbps 11n Wi-Fi USB Adapter
* Lb-link 150mbps Mini USB 802.11n/g/b Wireless Adapter with Antenna

## Installing the Open Roberta Server
### Requirements
Requirements to install the Server on your Raspberry Pi:
* Git: preinstalled
* JDK: `$ sudo apt-get install openjdk-7-jdk`
* Maven:   
  `$ wget http://ftp.halifax.rwth-aachen.de/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz`   
  `$ sudo tar -xzvf /path/to/apache-maven-3.3.9-bin.tar.gz`   
  `$ sudo mv apache-maven-3.3.9 /opt/`   
  `$ sudo nano /etc/profile.d/maven.sh`   
  edit the file so it looks like this:    
  `export M2_HOME=/opt/apache-maven-3.3.9`  
  `export PATH=$PATH:$M2_HOME/bin`  
   quit and save, then logout and log back in.

Create a directory for the Open Roberta Lab:  
`$ mkdir OpenRobert` e.g.   
`$ cd OpenRoberta`   

### Get the Sources via Git
Clone the sources     
`$ git clone https://github.com/OpenRoberta/robertalab.git`     
... this might take a while ...  
`$ cd robertalab`  

or   
### Get the Sources via Download (faster)
`$ wget https://github.com/OpenRoberta/robertalab/archive/master.zip`  
... this might take a while ...    
`$ unzip master.zip`  
`$ rm master.zip`  
`$ cd robertalab-master`

### Build the Application
`$ cd OpenRobertaParent`   
`$ mvn clean install -DskipTests`   
... this might also take a long while ...
```
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary:
[INFO]
[INFO] RobertaParent ...................................... SUCCESS [ 52.037 s]
[INFO] Resources .......................................... SUCCESS [  0.059 s]
[INFO] OpenRobertaShared .................................. SUCCESS [04:30 min]
[INFO] OpenRobertaRuntime ................................. SUCCESS [01:48 min]
[INFO] EV3Menu ............................................ SUCCESS [ 28.291 s]
[INFO] OpenRobertaRobot ................................... SUCCESS [05:27 min]
[INFO] OpenRobertaServer .................................. SUCCESS [02:58 min]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 16:08 min
[INFO] Finished at: 2015-12-26T18:08:29+01:00
[INFO] Final Memory: 38M/104M
[INFO] ------------------------------------------------------------------------
```
`$ cd ..`
  
## Start/Stop the Server
The start script for the server checks for a 64 bit Java version. We have to deactivate this test to use the script:   
`$ sudo nano ora.sh`   
find the line with   
`_checkJava;`   
add a # in front that it looks like   
`#  _checkJava;`  
save and quit.
   
`$ ./ora.sh --start` starts the server  
Usually the whole process is logged on the screen. However, if you want to save your logs to a file start the server with      
`./ora.sh --start > log.txt &`  
The process will then run in the background and all system messages will be written in the textfile log.txt.


`Ctrl` + `c` stops the server  
or if your server is running in the background find the process id with     
`$ pidof java`  
`1385` e.g.  
`$ kill 1385` stops the server



