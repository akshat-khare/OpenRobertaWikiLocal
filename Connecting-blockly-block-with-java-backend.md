In order to connect blockly blocks with java backend, two things are necessary, first, to map the blockly block to java class and second, to implement the java class.

From the robot properties file (found at Robot<Name>/src/main/properties):

# block types, that are added by this robot. Syntax (for category, see enum Category):
# blockType.<unique-name-of-the-block-type> = <category>,<full-path-of-implementing-class>,<blockly-xml-element-name-1>,...,<blockly-xml-element-name-n>

blockType.VOLTAGE_SENSING=SENSOR,de.fhg.iais.roberta.syntax.sensor.botnroll.VoltageSensor,robSensors_battery_voltage

A relation is one java class to many blockly blocks. What is important is to give a unique name (here VOLTAGE_SENSING) that will later be used in java and put the correct blockly block name to the end. The full path of java class is user specific and is based on the project structure. Usually description of sensors and actuators goes to syntax package and code generation for robots to syntax.codegen.

From java side it is possible to get the blockly block by invoking BlockTypeContainer.getByName("VOLTAGE_SENSING")