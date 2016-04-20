These information are for the guy who is deploying the system on the official server.
Run the build with the deployment profile in maven:

```
cd OpenRobertaParent
mvn clean install -P deployofficialserver
```

This will make sure that the correct lejos EV3Menu is distributed by the upload function on the server.
The menu will connect directly to lab.open-roberta.org. The menu can be toggled to the custom host selection in the system sub menu.

(If we decide to move the menu to a different repository or exclude it from the maven build, this information may be outdated!)