### What you need
* Java JDK 1.7, 1.8 will **not** work currently
* Maven 3.2.x, 3.3.3 works fine
  * for Linux users:  
    `wget http://ftp.halifax.rwth-aachen.de/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz`
### Get robertalab
* clone the repository with `git clone https://github.com/OpenRoberta/robertalab.git`   
  or   
* download the repository [here](https://github.com/OpenRoberta/robertalab/archive/master.zip) and unzip it

License information is available in the docs folder.

### Compilation and build
1. `$ cd robertalab/OpenRobertaParent` move from the root folder to the folder of the (maven) parent project
1. `$ mvn clean install` or `$ mvn clean install -DskipTests` if you don't want to run all the tests
1. Get a coffee! Might take a couple of minutes.
1. A successful build looks like:
```
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary:
[INFO] 
[INFO] RobertaParent ...................................... SUCCESS [  0.326 s]
[INFO] Resources .......................................... SUCCESS [  0.007 s]
[INFO] OpenRobertaShared .................................. SUCCESS [  2.415 s]
[INFO] OpenRobertaRuntime ................................. SUCCESS [  1.020 s]
[INFO] EV3Menu ............................................ SUCCESS [  0.665 s]
[INFO] OpenRobertaRobot ................................... SUCCESS [  5.727 s]
[INFO] OpenRobertaServer .................................. SUCCESS [  3.521 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------ 
```
### Start the server
`$ cd ..` return to the root folder
* Starting your own server instance, if a unix-like shell is available (on either lin* or win*).   
  `$ ./ora.sh --start` start the server, using default properties. Use --help for more options.   
  or  
* `$ java -cp target/resources/\* de.fhg.iais.roberta.main.ServerStarter` 

### Check the server
Start your browser at `localhost:1999`

### That's it!