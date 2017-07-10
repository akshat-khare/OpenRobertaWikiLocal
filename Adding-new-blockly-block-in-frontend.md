In order to add blockly blocks to OpenRoberta the first thing you need is to clone `https://github.com/OpenRoberta/blockly.git`.
Inside this repository there is a folder blocks that contains all javascript files containing blocks that will get merged together on build stage. Go inside the 'blocks' folder and choose an appropriate file (currently files are named after robots or grouped by some logic). If you feel that your blocks fall into some specific group that is not present, just create a new file. Typically files are named <robot>Actions.js <robot>Sensors.js and so on.

makeblockActions.js is a small file that can serve as an exmaple:

`/**
 * @fileoverview Action blocks for MakeBlock.
 * @requires Blockly.Blocks
 * @author Evgeniya
 */

'use strict';

goog.provide('Blockly.Blocks.makeblockActions');

goog.require('Blockly.Blocks');

Blockly.Blocks['makeblockActions_leds_on'] = {
    /**
     * Turn bricklight on.
     *
     * @constructs makeblockActions_leds_on
     * @this.Blockly.Block
     * @param {String/dropdown}
     *            SWITCH_COLOR - Green, Orange or Red
     * @param {Boolean/dropdown}
     *            SWITCH_BLINK - True or False
     * @returns immediately
     * @memberof Block
     */
    init : function() {
        var ledSide = new Blockly.FieldDropdown([ [ 'Left', 'Left' ], [ 'Right', 'Right' ] ]);
        this.setColour(Blockly.CAT_ACTION_RGB);
        this.appendValueInput('COLOR').appendField(Blockly.Msg.LED_ON).appendField(Blockly.Msg.BRICKLIGHT_COLOR).setCheck('Colour').appendField(ledSide, 'LEDSIDE');
        this.setPreviousStatement(true);
        this.setNextStatement(true);
        this.setTooltip(Blockly.Msg.LED_ON_TOOLTIP);
    }
};`

`Blockly.Blocks['makeblockActions_leds_on']` this starts a block definition, makeblockActions_leds_on is the blocklyu block name as it appears client side. One must provide init function in order for the block to be constructed. There is a number of predefined elements that could be used, like FieldDropdown or checkboxes. 

Play around with this simple block to see how it changes. You can observe the changes to the block by opening playgorund.html from 'tests' folder. If you have added a new javascript file, do not forget to modify the html page, so it would include your new script:

`<script src="../blocks/makeblockActions.js"></script>`

Another important thing in the playground is that blocks are grouped in toolboxes, so in order to actually be able to use the block it must be put in the appropriate toolbox:

`<category name='TOOLBOX_SENSOR' svg="true">
        <block type='makeblockSensors_light'></block>
        <block type='makeblockSensors_ambientlight'></block>
        <block type='bob3Sensors_irlight_getSample'>`

The above example adds blocks of given types (see blockly block name above) to TOOLBOX_SENSOR toolbox.