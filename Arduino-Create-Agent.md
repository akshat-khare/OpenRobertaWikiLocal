With robots that are arduino compatible there is a possibility to utilise Arduino Create Agent for transferring the HEX of the program to the board. Currently several robots already support this feature and automatic detection and connection to the robot is done by Open Roberta.

In order to use Create Agent one must install it first. The last windows release that can be found in github repository seems to be broken, but the installer that can be downloaded from the Arduino Web Editor page is (was) working. 

Links to installers:

* [For Windows](http://downloads.arduino.cc/CreateBridgeStable/ArduinoCreateAgent-1.1-windows-installer.exe)
* [For Linux](http://downloads.arduino.cc/CreateBridgeStable/ArduinoCreateAgent-1.1-linux-x64-installer.tar.gz)

A couple of things need to be changed for the Create Agent to work with RobertaLab:

* public key for signing the command line
* origins URL (if you are not using lab.open-roberta.org)

You can get a file from OpenRoberta git repository from Resources folder. Modify accordingly your origins URL. Do not modify the key though.