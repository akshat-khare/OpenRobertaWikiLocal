We have been selected as an org for Google Summer of Code 2018!

## Application instructions
Before you [apply](https://summerofcode.withgoogle.com/organizations/6256279438229504/), please have a look at what we have already developed. Play around with our [lab](https://lab.open-roberta.org), fork the robertalab repository, try to install and run it locally. Feel free to ask us for help, if necessary.

If you have already committed to an Open Source project, please provide a link to this in your application. If you haven't, no problem, but maybe you can provide us some other samples of your programming experience. Also student's projects are welcome.

Have a look at our list of proposals for GSOC. If you have another good idea, don't hesitate to come up with your own project proposal. Maybe you would like to discuss it with us before you apply, please use [Gitter](https://gitter.im/open-roberta-lab/GSoC).



## Support for custom sensor/actor blocks

Many robots support a large variety of hardware addons. Even robots like the LEGO MINDSTORMS® EV3 can be used with 3rd party sensors and actuators. In this project the student would design a system that lets the user create new blocks to support additional hardware.

Currently such changes require modification on the server side and a new release (see the two articles on blockly - [Adding new blockly block in frontend](https://github.com/OpenRoberta/robertalab/wiki/Adding-new-blockly-block-in-frontend),[Connecting blockly block with java backend](https://github.com/OpenRoberta/robertalab/wiki/Connecting-blockly-block-with-java-backend)). A lot of the code that is needed to handle a new block on the server and on the web-frontend is quite similar though.

A first step would be to add infrastructure to reduce code duplication in the project. Later this can be expanded to let users define their own blocks. Initially such custom blocks would be stored with the project. A better way would be to store them in the user's account (if logged in). A stretch goal would be to add support for contributing/sharing blocks.

On the technical side, the project involves:
* code generators for the new blocks (maybe based on some templating)
* a way to include custom library code (e.g. on the Arduino side)
* adding those custom blocks to the blockly toolbox in the web ui

Mentor: Stefan (ensonic)

## Support for custom assets (EV3, NXT)

The Open Roberta® Lab provides a few built-in pictures, melodies and toolboxes. For more advanced users it would be nice to allow them to upload their own.

As part of the project, you'd need to:

* design a way to store assets in the project
* ensure uploaded data is converted into a suitable format for the robot
* design UI upload dialogs
* add a "play sound" block
* add a “show custom picture block”
* provide a way to record sounds using the microphone

[GitHub Ticket1](https://github.com/OpenRoberta/robertalab/issues/90)
[GitHub Ticket2](https://github.com/OpenRoberta/robertalab/issues/216)

Mentor: Evgeniya


## Interactive source code view (Medium/Hard)

The Open Roberta® Lab using the graphical programming language NEPO provides an easy access in the world of programming robot system without any prior programming experience. In parallel to the program created with the NEPO language one can also see the corresponding source code generated for the specifiy robot system. Currently in the source code view the whole code is shown.

We would like to add code folding and hide boilerplate code by default, so that new users are not distracted. In addition we would like to link the graphical blocks to the generated code, and the possibility by changing parts of the generated source code the NEPO representation of the program to change.

On the technical side, the project involves:

* extending the code generators (written in Java) to link block ids to character ranges in the generated code
* adding UI support for highlighting and jumping to code when a block is clicked
* identifying and hiding boilerplate code (eg when block id is invalid)
* optionally, linking the block parameters to the parameters in the generated code
* optionally, improving the readability of generated code

Mentor: Kostadin, Beate, Reinhard


## The NEPO debugger (Medium/Hard)

All modern editors have possibility of debugging your code. In our Open Roberta® Lab we would like to have the option of debugging a program written in the NEPO language for robots system (EV3) that have real time connection with the Open Roberta Lab. In the first step of this project the student would design a system that allows displaying on the client the current executed block as well as the readings from all the connected sensors. For the second step (optionally) integrated more traditional options for a debugger (controlling the execution of the program, evaluating the variables.)

On the technical side, the project involves:
* adding UI support for highlighting the current executed code
* adding UI support for showing the sensor values

Mentor: Kostadin, Reinhard

## The Open Roberta Lab standalone version
The number of users of the lab increases daily. Nevertheless their are still a lot of schools with no or limited internet access. Is their a way to help them?
One idea could be to integrate the server in a web view and run it fully locally. Ideally this will customize the web-ui to e.g. hide the menu for user-login etc.
We also think about to combine it with parts of the USB program to allow working with local robots (since otherwise e.g. the lego-ev3 would try to connect to the online server).

If all that work, it would be interesting to e.g. package this as a mobile app (e.g. for android).

Mentor: Beate, Stefan (ensonic)

## Multiple robots in the simulation (Medium)

The Open Roberta® Lab provides ​a simulation, where our users can test their programs without a real robot. Currently the simulation only supports one board and we would like to extend it in such a way that it is possible to simulate behavior of two or more robots. First step would be an implementation of such a system with a static robot, e.g. Calliope, where all multiagent interaction is restricted by message exchange.
Here, the connection between two client programs on the server has to be established (including UI).
Further steps would include multiagent simulation for driving robots like EV3, NXT and possibly Bot'n Roll.

Mentor: Evgeniya, Kostadin, Beate