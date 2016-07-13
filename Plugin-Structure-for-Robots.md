The OpenRoberta server components have been refactored to allow an easy
integration of new robots. The simple idea is, to put all robot-specific
stuff into a project and make a jar out of it. At server startup time the
available robots are determined. The main entry point for every robot is an implementation of the interface IRobotFactory.

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

To be continued in a moment ...