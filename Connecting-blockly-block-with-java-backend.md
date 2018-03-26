In order to connect blockly blocks with java backend, two things are necessary, first, to map the blockly block to java class and second, to implement the java class.

### Mapping a Blockly block to a java class

Depending on the type of the blockly block the mapping is done in OpenRobertaRobot/src/main/resources/Robot.propertis or in specific robot property (found at Robot<Name>/src/main/properties). All the blockly blocks that are common to all robot types are mapped in OpenRobertaRobot project, and all robot specific block are mapped in the robot specific property.

Example of a property that maps a blockly block to java class:
```
# block types, that are added by this robot. Syntax (for category, see enum Category):
# blockType.<unique-name-of-the-block-type> = <category>,<full-path-of-implementing-class>,<blockly-xml-element-name-1>,...,<blockly-xml-element-name-n>

blockType.VOLTAGE_SENSING=SENSOR,de.fhg.iais.roberta.syntax.sensor.botnroll.VoltageSensor,robSensors_battery_voltage
```
In order the mapping to be successful one has to:
*  provide a unique pairing name (ex. **blockType.VOLTAGE_SENSING**) that will later be used in java and put the correct blockly block name to the end
*  full path of java class (it is user specific and is based on the project structure), usually description of sensors and actuators goes to syntax package and code generation for robots to syntax.codegen
*  description for the type of the block (ex. SENSOR, ACTOR, EXPR, ...)
*  name(s) of the blockly block(s) that we want to map

**Note**: A relation is one java class to many blockly blocks

### Implement Java class that corresponds to Blockly block(s)
