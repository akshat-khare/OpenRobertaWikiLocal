### Why
A lot of people, teachers and students, around the world have no good internet connection or other good reasons not to use our online server at [https://lab.open-roberta.org](https://lab.open-roberta.org). This tutorial explains how to setup the server on lokal system, either as standalone version (not recommended), or as local network installation, e.g. in classrooms or maybe in a school or intranet network (sorry, no real experience in this).

You can install the Open Roberta Lab on several different systems. We recommend to install it on a linux system like ubunto, which is easy, but depending on what you want to use also windows or Mac OS X can be an alternative. So please read carefully what you have to install besides the Open Roberta Lab, maybe you don't need all of this.

### Get the Open Roberta Lab
* download the binaries from the latest release [here](https://github.com/OpenRoberta/robertalab/releases). Please choose the latest embedded version `embedded_x.y.z.zip`, which means the database is running in an embedded mode.  

License information is available here [https://github.com/OpenRoberta/robertalab/tree/master/Resources](https://github.com/OpenRoberta/robertalab/tree/master/Resources). Please read the file LICENCE and NOTICE carefully. If you have questions please contact us.

* extract the zip file and copy the content of the the embedded-x.y.z folder to your desired location, e.g. into a new folder "OpenRobertaLab". If this is your first installation please copy the empty database db-x.y.z into the same folder next to the other folders and scripts, if not, make sure the complete database folder from your previous version is copied into the same folder (or stays there).

### Get the necessary programs / packages for your system, used by the Open Roberta server:
* make sure that Java Runtime Environment (JRE) is available. Open a command prompt and type `java -version`, if it is already available then the output is something with `java version "1.8.a_b"`. It should be something with java version 1.8... otherwise check the oracle websites for how to get it.

**Install now all the programms needed for compilation of code for the different supported robot systems, maybe you do not need all of them**
* on linux systems (Ubuntu)
** Arduino based robots
*** `sudo apt-get install libusb-0.1-4`
*** `sudo apt-get install gcc-avr binutils-avr gdb-avr avr-libc avrdude`
** for NXT
*** `sudo apt-get install nbc`
** for Calliope
*** `sudo apt-get install gcc-arm-none-eabi srecord libssl-dev`
** for micro:bit
** `pip install uflash`