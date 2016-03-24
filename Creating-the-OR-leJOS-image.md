Requirements: A computer with a Linux(!) operating system, internet connection
To create a new Open Roberta leJOS image, run maven install on the project first, to have all dependencies available in the correct places.

```
cd OpenRobertaParent
mvn clean install -P deployofficialserver
```
(This will preset the EV3Menu to directly connect to lab.open-roberta.org).

Afterwards run ```CreateImage.sh``` in the directory```<repo>/Resources/image```.
You can pass a parameter to the script as the version number, default version is 1.3.2. Example:

```
cd Resources/image
sudo sh CreateImage.sh 1.4.0
```

This will download the original leJOS files and modify the image. You will get a file named OpenRobertaFirmware-\<version\>-release.zip next to the script. The script is only for Linux!!