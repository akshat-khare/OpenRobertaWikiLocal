Eclipse setup is fairly simple,

* Open eclipse and use File->Import to import new maven projects
* Select the root directory and tick all related projects to import
* After importing go to Window->Preferences->Java->Code Style->Formatter and import java formatter from Resources folder
* Do the same for Javascript
* Go to OpenRobertaServer project (de.fhg.iais.roberta.main) locate and run as java program ServerStarter.java

You are now running OpenRoberta server locally on tour machine and can edit all the code and see the effect in the browser at localhost:1999

If you encounter an error with "...db parent folder OpenRobertaServer..." go to run configurations in Eclipse (drop-down arrow next to green run button), select ServerStarter and go to Arguments. In this tab add -d database.parentdir=<path to git repository>\OpenRobertaServer\ argument and now the databse will be found. If you have errors with hibernate, add this argument as well: -d hibernate.connection.url=jdbc:hsqldb:file:<path to git repository>\OpenRobertaServer\db-<insert version here>\openroberta-db

After updating certain resources or if something gets cached and does not change, right click on any project and go to Maven->Update project, in the window that pops up, select all related projects and update.