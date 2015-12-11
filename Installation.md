### What you need
* Java JDK 1.7 
* Maven 3.2.x

### Get robertalab
* clone the repository with `git clone https://github.com/OpenRoberta/robertalab.git`

  or
* download the repository [here](https://github.com/OpenRoberta/robertalab/archive/master.zip) and unzip it

License information is available in the docs folder.

### Compilation and build
1. `$ cd /robertalab/OpenRobertaParent` move from the root folder to the folder of the (maven) parent project
1. `$ mvn clean install` or `$ mvn clean install -DskipTests` if you don't want to run all the test
1. Get a coffee! Might take a couple of minutes.
1. A successful build looks like:

`[INFO] ---------------------------------------`

`[INFO] Reactor Summary:`

`[INFO] RobertaParent ..................SUCCESS`

`[INFO] OpenRobertaShared ..............SUCCESS`

`[INFO] OpenRobertaServer ..............SUCCESS`

`[INFO] OpenRobertaRuntime .............SUCCESS`

`[INFO] ---------------------------------------`

`[INFO] BUILD SUCCESS`