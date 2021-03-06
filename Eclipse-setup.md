Eclipse setup is fairly simple. Before we import the Open Roberta Lab project into the eclipse workspace first we have to modify some settings.

### Adding custom code style formatter 

We have designed our code style formatter for Java and JavaScript code. 

* Go to **Window->Preferences->Java->Code Style->Formatter** and import _openRobertaJava_ formatter from _robertalab/Resources/formatter_ folder
* Do the same for Javascript

### Setup 'save actions'

Another thing to configure in Eclipse is to setup 'save actions' in Preferences->Java->Editor. They should be all ticked with 'Format all lines selected'. Actions themselves should be the following:

* Add 'this' qualifier to unqualified field accesses
* Change non static accesses to static members using declaring type
* Change indirect accesses to static members to direct accesses (accesses through subtypes)
* Convert control statement bodies to block
* Add final modifier to private fields
* Use lambda where possible
* Remove unnecessary parentheses
* Remove unused imports
* Add missing '@Override' annotations
* Add missing '@Override' annotations to implementations of interface methods
* Add missing '@Deprecated' annotations
* Remove unnecessary casts
* Remove unnecessary '$NON-NLS$' tags
* Remove trailing white spaces on all lines
* Correct indentation

Here are the images which show what all fields are to be ticked.
<p align="center">
  <img src="/img/1.png" width="350"/>
  <img src="/img/2.png" width="350"/>
  <img src="/img/3.png" width="350"/>
  <img src="/img/4.png" width="350"/>
  <img src="/img/5.png" width="350"/>
</p>

If you wish to counter long package names and provide somewhat clearer package explorer view, then go to Window -> Preferences -> Java -> Appearance and tick the "Abbreviate package names" checkbox. A suggested template for this is as follows:

* de.fhg.iais.roberta={rob}
* de.fhg.iais.roberta.syntax={syntax}
* de.fhg.iais.roberta.mode={mode}
* de.fhg.iais.roberta.factory={factory}

### Importing the project

* Open eclipse and use File->Import to import new maven projects
* Select the OpenRobertaParent directory and tick all related projects to import
* Right click OpenRobertaServer project, go to **properties -> java build path -> projects** and add all robot plugin projects and click apply.

You are now running OpenRoberta server locally on tour machine and can edit all the code and see the effect in the browser at localhost:1999

### Start the server
* Go to OpenRobertaServer project (de.fhg.iais.roberta.main) locate and run as java program ServerStarter.java
  * This will immediately start the server, but paths to the compiler are not correct until now
  * Terminate the server with a click on the red square
* Go to run configurations in Eclipse (drop-down arrow next to green run button), select ServerStarter and go to Arguments. 
  * in Program Arguments add: `-d database.parentdir=<path to git repository>/OpenRobertaParent/OpenRobertaServer/` 
  * in Working directory: Check Other and add: `<path to your git repo>/robertalab/`



### Possible errors
If you encounter an error with hibernate go to run configurations in Eclipse (drop-down arrow next to green run button), select ServerStarter and go to Arguments, add this argument as well: 
`-d hibernate.connection.url=jdbc:hsqldb:file:<path to git repository>/OpenRobertaParent/OpenRobertaServer/db-<insert version here>/openroberta-db`

After updating certain resources or if something gets cached and does not change, right click on any project and go to Maven->Update project, in the window that pops up, select all related projects and update.

If you encounter "name of robot" has invalid factory - class not found exception - this is due to the fact that your classpath is not updated. Right click OpenRobertaServer project, go to properties -> java build path -> projects and add all robot plugin projects and click apply. Now all needed classes should be on the class path.



