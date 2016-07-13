# Overview

This text combines the description of the actual robot-plugin-structure and ideas for
further refactorings. If the refactorings are done, the text has to be updated to fit to
the actual implementation.

The OpenRoberta server components have been refactored to allow an easy
integration of new robots. The simple idea is, to put all robot-specific
stuff into a project and make a jar out of it. At server startup time the
available robots are determined. The main entry point for every robot is an
implementation of the interface IRobotFactory.

Some notes:
* at the moment we assume, that there are _no_ robot-specific _blockly blocks_.
  This may change in the future.
* the front end issues Rest calls to the server. The Rest calls are processed
  by jetty/jersey. Dependency injection into the request objects is done with guice.
  Thus the injection becomes robot-aware.
* in a sandwich-like structure a robot-specific project
    + uses the OpenRobertaRobot project (lower in the hierarchy) as a base. Here interfaces are found
      (IRobotFactory e.g.), which the robot-specific project has to implement
    + is used by the OpenRobertaServer project (higher in the hierarchy) to deliver the robot specific functionality.

# Startup

When the server starts (class ServerStarter), the openRoberta.properties file is read.
In this file all robots available have to be declared. E.g.
'''
robot.plugin.1.name = ev3
robot.plugin.1.id = 42
robot.plugin.1.factory = de.fhg.iais.roberta.factory.EV3Factory
'''
From this data a Map<String,IRobotFactory> is build and made available for guice. If a robot is added to OpenRoberta,
the property file has to be changed.

>> The _id_ is annoying. But to remove it, some further refactorings which touch the database are needed **Help wanted**

>> The robots could/should be auto-discovered. There are several solutions (hibernate, jersey, stack-overflow, ... :-).
>> The java reflection API does not support it. Thus there is no solution agreed by a larger community.
>> Do you have proposals for auto-discovery (frameworks)? **Help wanted**

# IRobotFactory

The entry point for a robot is an implementation of the IRobotFactory interface (or an extension of the abstract class
AbstractRobotFactory). The following assumptions are made:
* a factory has a constructor _public XyzFactory(RobotCommunicator robotCommunicator, Integer robotId)_. This constructor 
    + the robotCommunicator encapsulates the state of the communication of server and robots (or server and the
      so-called UsbPrograms if the robot is not able to communicate with the server directly, e.g. NXT)
    + the robotId is used to access the blockly toolbox and the robot configuration in the database.
      The robotId should be removed as soon as possible (see further remarks elsewhere)
* a factory supplies a lot of enumerations for the compilation process. This includes
    + ports for sensors and actors
    + modes for a specific sensor (e.g. ColorSensor modes) and actors
    + and more
* in the robot plugin project (e.g. RobotEv3) each enumeration (e.g. ColorSensorMode) is defined:
'''
public enum ColorSensorMode implements IColorSensorMode {
    COLOUR( "getColorSensorColour", "ColorID" ),
    RED( "getColorSensorRed", "Red" ),
    RGB( "getColorSensorRgb", "RGB" ),
    AMBIENTLIGHT( "getColorSensorAmbient", "Ambient" );
'''
* each enumeration implements an interface defined in OpenRobertaProject (e.g. IColorSensorMode).
  Only the set of these interfaces is used by the server. Thus the server becomes independant of the concrete robots.

>> the robot factory is flooded by the many access operations for enums. The factory should have a getter for an
>> EnumProvider (better name?), which then gets these methods. **Help wanted**

* it is expected, that each robot has a robot-specific property file
  (e.g. RobotEv3 has EV3.properties in src/main/resources). This is needed for different purposes, e.g.
  if scripts have to run for background compilation (EV3 lejos and NXT have a need for directories in which
  temp files are stored; EV3DEV doesnt need that).

>> this property file should contain XML data, that is robot specific and at the moment stored in the database:
>> the 2 toolboxes for _beginner_ and _expert_ and the _robot configuration_. This data should be extracted from the
>> data base and put into the property file. The Rest calls returning this data to the front end have to be adapted
>> for this **Help wanted**
