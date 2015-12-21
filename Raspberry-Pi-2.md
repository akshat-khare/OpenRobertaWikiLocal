## under construction
<p align="center"><em>It is highly recommended to checkout the raspberry's websites, especially <a href="https://www.raspberrypi.org/help/">https://www.raspberrypi.org/help/</a>, where you will find all information about the necessary steps to get started.</em></p>


## First time setup for system and WiFi router

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
* NOOBS easy installer for Raspbian (and others). Use this, if you have no keyboard or monitor available -> see headless installation
* NOOBS Lite network installer for Raspbian (and others)
* RASPBIAN  
 
We have tried all of them, they work without any issues.

#### Headless installation
If you don't have a monitor and/or mouse and keyboard on hand, download [NOOBS easy install for Rasbian](https://downloads.raspberrypi.org/NOOBS_latest), unzip and copy the image to the SD card and open the file `recovery.cmdline` with a simple editor.

Add ` silentinstall` at the end of the first (and only) line, so that it looks like this   
`runinstaller quiet ramdisk_size=32768 root=/dev/ram0 init=/init vt.cur_default=1 elevator=deadline silentinstall` [(Paul Lunow)](http://www.interaktionsdesigner.de/2014/raspberry-pi-ohne-monitor-tastatur-und-maus-in-betrieb-nehmen/)

Plug in the network and power cable. After the first boot (ca. 30 min, only the red LED is on) your Raspberry Pi will be visible in your routers DHCP table as raspberry. You can now easily log in to your raspberry via ssh from any computer/laptop in your local network.



### Configuring the Raspberry Pi 

Now slot in the SD card into your Raspberry Pi 2, connect a USB-Keyboard and Ethernet cable as well as a monitor and finally your micro usb power supply. Your Raspberry Pi 2 will turn on and boot from the SD card. Now login.

Default login information is:
```
User: pi
Password: raspberry
```
#### raspi-config settings
1. `$ sudo raspi-config`
  1. to change Keyboard Layout (Internationalisation Options-> Change Keyboard layout)
  1. expand fileysytem to make sure there is enough space on your SD card.
  1. Change user Password, if you want to. Your username will still be Pi.
  1. Overclock. Set to “medium” if you go any further you will need cooling for the raspberry pi.
  1. if you want to work with SSH (e.g. Putty), go into advanced options->SSH->Enable.
  1. Advanced Options->Memory Split. Set to 16.
1. Back at the raspi-config home screen click “finish” (2x Tab)
1. reboot your Raspberry Pi with 
`$ sudo reboot`

#### update
After the reboot make sure your Raspberry Pi is up-to-date. You will require Internet connection for this!
```
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo rpi-update
$ sudo reboot
```

#### static IP address
collect the data you need for setting up a static IP for your Raspberry Pi. Look up the following numbers:
 
1. `$ ifconfig`
1. Note the following numbers: 
  1. inet addr
  1. Bcast
  1. Mask
1. `$ netstat -nr`
1. note the following numbers: 
  1. Gateway
  1. Destination
1. Edit the Network Configuration with:   
   `$ sudo nano /etc/network/interfaces`
1. Change the line      
   `iface eth0 inet dhcp`   
   to   
   `iface eth0 inet static`   
1. Below this line enter you gathered data with
```
address <insert number you noted by inet addr>
netmask <insert number you noted by Mask>
network <insert number you noted by Destination>
broadcast <insert number you noted by Bcast>
gateway <insert number you noted by Gateway>
```
1. Save and Quit (CTRL+X and  type y to save changes)
1. To remove existing leases run `$ sudo rm /var/lib/dhcp/*`   
   Then `$ sudo reboot`
1. Check your settings with ifconfig or ping your Gateway Address with `ping xxx.xxx.x.xxx –c10`

## Installing the Open Roberta Server
### Requirements
Requirements to install the Server on your Raspberry Pi:
* Git: preinstalled
* JDK: `$ sudo apt-get install openjdk-7-jdk`
* Maven: `$ sudo apt-get install maven`

Sometimes you may experience conflicts with the maven version you get with "apt-get" This is the alternative installation, which will install version 3.2.5 on the Raspberry Pi
```
$ wget http://www.mirrorservice.org/sites/ftp.apache.org/maven/maven-3/3.2.5/binaries/apache-maven-3.2.5-bin.tar.gz
$ sudo tar -xzvf /path/to/apache-maven-3.2.5-bin.tar.gz
$ sudo mv apache-maven-3.2.5 /opt/
$ sudo nano /etc/profile.d/maven.sh
```
edit the file so it looks like this:
```
export M2_HOME=/opt/apache-maven-3.2.5
export PATH=$PATH:$M2_HOME/bin 
```
quit and save, then logout and log back in

### Install via Git
Next you clone your directory   
`$ git clone https://github.com/OpenRoberta/robertalab.git`     
... this might take a while ...   

check the branches   
`$ cd robertalab/`  
`$ git branch`   
`*master`

build the application:   
`$ cd /OpenRobertaParent`   
`$ mvn clean install -DskipTests`   
... this might also take a while ...
  
start the server:
`$ cd ..`   
`$ ./ora.sh --start`
Usually the whole proccess is logged on the screen. However, if you want to save your logs to a file this is how you do it:   
`./ora.sh --start > log.txt &`  
The process will then run in the background and all system messages will be written in the textfile log.txt.

stop the server:
`Ctrl` + `c`   
or if your server is running in the background:   
`ps -e|grep java`

## Wifi Access Point
If not done yet, plug the Wifi Adapter into the Raspberry pi.
Check if its connected with 
ifconfig
(You should be able to see a block with wlan0 at the beginning.)
install and setup the software
Install the Software for your access point with
Sudo apt-get install hostapd isc-dhcp-server
Edit the file that sets up the DHCP server with
Sudo nano /etc/dhcp/dhcpd.conf
Change the lines
option domain-name “example.org”;
option domain-name-servers ns1.example.org, ns2.example.org;
To
#option domain-name “example.org”;
#option domain-name-servers ns1.example.org, ns2.example.org;
Change the lines
# If this DHCP server is the official DHCP server for the local
# network, the authoritative directive should be uncommented.
#authoritative
to
# If this DCHP server is the official DHCP server for the local
# network, the authoritative directive should be uncommented.
authoritative
(remove last #)
At the end of the Script add the following lines:
subnet 192.168.42.0 netmask 255.255.255.0 {
range 192.168.42.10 192.168.42.50;
option broadcast-address 192.168.42.255;
option routers 192.168.42.1;
default-lease-time 600;
max-lease-time 7200;
option domain-name "local";
option domain-name-servers 8.8.8.8, 8.8.4.4;}Save with CTRL-X then Y then RETURN
Open the following file:
sudo nano /etc/default/isc-dhcp-server
Find the line that says
INTERFACES=””
and change it to
INTERFACES=”wlan0”
Close and Save

setup static IP for Wlan0
Open the following file
sudo nano /etc/network/interfaces
Change the line
auto wlan0
To
#auto wlan0
Add the lines
iface wlan0 inet static
 address 192.168.42.1
 netmask 255.255.255.0
Save the file
To assign the static IP address type
sudo ifconfig wlan0 192.168.42.1
configure the Access Point
Run
sudo nano /etc/hostapd/hostapd.conf
Type the following in there
interface=wlan0
driver=rtl871xdrv
ssid=Pi_AP
hw_mode=g
channel=6
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=Raspberry
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
(The text behind ssid= can be changed to the network name you want to be displayed. The password can be changed. Fill in your password behind wpa_passphrase= )
Save the file. Make sure the lines don’t have extra spaces or tabs at the end!
Now tell the Raspberry Pi where to find this configuration.
run:
sudo nano /etc/default/hostapd
Change the line
#DAEMON_CONF=””
to
DAEMON_CONF=”/etc/hostapd/hostapd.conf”
Save the file and exit
allow multiple clients to connect
 Run
Sudo nano /etc/sysctl.conf
Add the following line to the bottom:
net.ipv4.ip_forward=1
Save and quit.
Run:
sudo sh –c “echo 1 > /proc/sys/net/ipv4/ip_forward”
After that, run the following commands:
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
sudo iptables -A FORWARD -i eth0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i wlan0 -o eth0 -j ACCEPT
sudo sh –c “iptables-save > /etc/iptables.ipv4.nat”
run:
sudo nano /etc/network/interfaces
add
up iptables-restore < /etc/iptables.ipv4.nat
to the end

Update
This has to be done to update this to a version which supports the wifi adapter.
Type:
wget http://adafruit-download.s3.amazonaws.com/adafruit_hostapd_14128.zip
After this is done type:
unzip adafruit_hostapd_14128.zip
Move the old version away with:
sudo mv /usr/sbin/hostapd /usr/sbin/hostapd.ORIG
And move the new version there with:
sudo mv hostapd /usr/sbin
Set it up that its allowed to run with:
sudo chmod 775 /usr/sbin/hostapd
Test the access point host with:
sudo /usr/sbin/hostapd /etc/hostapd/hostapd.conf
You can now try to connect via another device. You should be able to see your network besides your other Wifi networks.
set up as a daemon
Run:
sudo service hostapd start
sudo service isc-dhcp-server start
then run:
sudo update-rc.d hostapd enable
sudo update-rc.d isc-dhcp-server enable
Check the status of the host AP server and the DHCP server with
sudo service hostapd staus
sudo service isc-dhcp-server status
If you are getting error messages try to remove the WPA-Supplicant with
sudo mv /usr/share/dbus-1/system-services/fi.epitest.hostap.WPASupplicant.service ~/
then reboot
the wifi acess point should now run whenever the Raspberry Pi is on.
How to access the server.
After you started the server via
java –cp “robertalab/OpenRobertaServer/target/resources/*” de.fhg.iais.roberta.main.ServerStarter
or via
cd robertalab/
./ora.sh --start
access the Server from another device by connecting to the Wifi Network you just created, go to a browser and type
192.168.42.1:1999
You should now be redirected to the Open Roberta Lab.
If you can't connect via this IP address type
ifconfig
and look at the "wlan0" block. Type the number behind "inet addr" into your Browser and add
:1999 
to the end.

You can disconnect the ethernet-cable, it is not neccessary to have, if you only want to work with the Open Roberta Lab. If you want to connect to the Internet via your Raspberry Pi connection, you have to leave the ethernet-cable attached
***