With robots that are arduino compatible there is a possibility to utilise Arduino Create Agent for transferring the HEX of the program to the board. Currently several robots already support this feature and automatic detection and connection to the robot is done by Open Roberta.

In order to use Create Agent one must install it first. The last windows release that can be found in github repository seems to be broken, but the installer that can be downloaded from the Arduino Web Editor page is (was) working. 

Links to installers:

* [For Windows](http://downloads.arduino.cc/CreateBridgeStable/ArduinoCreateAgent-1.1-windows-installer.exe)
* [For Linux](http://downloads.arduino.cc/CreateBridgeStable/ArduinoCreateAgent-1.1-linux-x64-installer.tar.gz)

A couple of things need to be changed for the Create Agent to work with RobertaLab:

* public key for signing the command line
* origins URL (if you are not using lab.open-roberta.org)

You can get a file from OpenRoberta git repository from Resources folder. Modify accordingly your origins URL. Do not modify the key though.

If you run into a problem that will be logged by the agent as "avrdude: ser_open(): can't open device "/dev/ttyACM0": Permission denied" then you have two solutions: temporary one, just do sudo chmod 666 /dev/ttyACM0 and a permanent one that is writing a udev rule. 

1. Add a createagent group:
sudo addgroup createagent
2. Add yourself to this group:
sudo usermod -a -G createagent <username>
3. Create a file 45-createagent.rules with the following content:

`# Bob3
SUBSYSTEM=="usb", ATTRS{idVendor}=="16c0", ATTRS{idProduct}=="0933", SYMLINK+="bob3", GROUP="createagent", MODE="0666"`

`# mBot
SUBSYSTEM=="usb", ATTRS{idVendor}=="1a86", ATTRS{idProduct}=="7523", SYMLINK+="mBot", GROUP="createagent", MODE="0666"`

`# BotNRoll
SUBSYSTEM=="usb", ATTRS{idVendor}=="10c4", ATTRS{idProduct}=="ea60", SYMLINK+="botnroll", GROUP="createagent", MODE="0666"`

4. Copy this file to /etc/udev/rules.d. From a console window type:
sudo cp 45-createagent.rules /etc/udev/rules.d

Now your robot should always have correct read/write permissions. You will probably need to reboot your computer once for the rules to take effect.