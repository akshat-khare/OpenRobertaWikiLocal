We will apply for Google Summer of Code 2018.

Keep your fingers crossed, that we get accepted ;-) ...

## Application instructions
Before you apply, please have a look at what we have already developed. Play around with our [lab](https://lab.open-roberta.org), fork the robertalab repository, try to install and run it locally. Feel free to ask us for help, if necessary.

If you have already committed to an Open Source project, please provide a link to this in your application. If you haven't, no problem, but maybe you can provide us some other samples of your programming experience. Also student's projects are welcome.

Have a look at our list of proposals for GSOC. If you have another good idea, don't hesitate to come up with your own project proposal. Maybe you would like to discuss it with us before you apply, please use our [mailing list](https://groups.google.com/forum/#!forum/open-roberta).



## Support for custom sensor/actor blocks

Many robots support a large variety of hardware addons. Even robots like the LEGO MINDSTORMS® EV3 can be used with 3rd party sensors and actuators. In this project the student would design a system that lets the user create new blocks to support additional hardware.

Initially such blocks would be stored with the project. A better way would be to store them in the user's account (if logged in). A stretch goal would be to add support for contributing/sharing blocks.

On the technical side, the project involves:
code generators for the new blocks (maybe based on some template)
a way to include custom library code (e.g. on the Arduino side)

Mentor: Stefan

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

Mentor: 


## Interactive source code view (Medium/Hard)

The Open Roberta® Lab using the graphical programming language NEPO provides an easy access in the world of programming robot system without any prior programming experience. In parallel to the program created with the NEPO language one can also see the corresponding source code generated for the specifiy robot system. Currently in the source code view the whole code is shown.

We would like to add code folding and hide boilerplate code by default, so that new users are not distracted. In addition we would like to link the graphical blocks to the generated code, and the possibility by changing parts of the generated source code the NEPO representation of the program to change.

On the technical side, the project involves:

* extending the code generators (written in Java) to link block ids to character ranges in the generated code
* adding UI support for highlighting and jumping to code when a block is clicked
* identifying and hiding boilerplate code (eg when block id is invalid)
* optionally, linking the block parameters to the parameters in the generated code
* optionally, improving the readability of generated code

Mentor:


## The NEPO debugger (Medium/Hard)

All modern editors have possibility of debugging your code. In our Open Roberta® Lab we would like to have the option of debugging a program written in the NEPO language for robots system (EV3) that have real time connection with the Open Roberta Lab. In the first step of this project the student would design a system that allows displaying on the client the current executed block as well as the readings from all the connected sensors. For the second step (optionally) integrated more traditional options for a debugger (controlling the execution of the program, evaluating the variables.)

On the technical side, the project involves:
* adding UI support for highlighting the current executed code
* adding UI support for showing the sensor values

Mentor:

## The Open Roberta Lab standalone version
The number of users of the lab increases daily. Nevertheless their are still a lot of schools with no or limited internet access. Is their a way to help them?
One idea could be to integrate the server in a web view and run it fully locally. We also think about to combine it with parts of the USB program.
TODO provide more ideas
