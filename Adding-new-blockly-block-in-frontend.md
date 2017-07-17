In order to add blockly blocks to OpenRoberta the first thing you need is to clone `https://github.com/OpenRoberta/blockly.git`.
Inside this repository there is a folder blocks that contains all javascript files containing blocks that will get merged together on build stage. Go inside the 'blocks' folder and choose an appropriate file (currently files are named after robots or grouped by some logic). If you feel that your blocks fall into some specific group that is not present, just create a new file. Typically files are named <robot>Actions.js <robot>Sensors.js and so on.

simSensors.js can serve as an exmaple:

[SimSensors](https://github.com/OpenRoberta/blockly/blob/master/blocks/simSensors.js)

`Blockly.Blocks['sim_touch_isPressed']` this starts a block definition, sim_touch_isPressed is the blockly block name as it appears client side. One must provide init function in order for the block to be constructed. There is a number of predefined elements that could be used, like FieldDropdown or checkboxes. 

Play around with this simple block to see how it changes. You can observe the changes to the block by opening playgorund.html from 'tests' folder. If you have added a new javascript file, do not forget to modify the html page, so it would include your new script:

`<script src="../blocks/simSensors.js"></script>`

Another important thing in the playground is that blocks are grouped in toolboxes, so in order to actually be able to use the block it must be put in the appropriate toolbox:

`<category name='TOOLBOX_SENSOR' svg="true">`
`<block type='sim_touch_isPressed'></block>`

The above example adds blocks of given types (see blockly block name above) to TOOLBOX_SENSOR toolbox.