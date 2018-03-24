The OpenRoberta software consists of a server component, sub modules for [robot plugins](https://github.com/OpenRoberta/robertalab/wiki/Plugin-Structure-for-Robots) and the web frontend.

# Server
The server side components are written in Java and located in the source tree under [OpenRobertaParent/OpenRobertaServer/src](https://github.com/OpenRoberta/robertalab/tree/develop/OpenRobertaParent/OpenRobertaServer/src).

Persistence is implemented using the [hibernate orm](http://hibernate.org/orm/) and related classes are defined under [OpenRobertaParent/OpenRobertaServer/src/main/java/de/fhg/iais/roberta/persistence](https://github.com/OpenRoberta/robertalab/tree/develop/OpenRobertaParent/OpenRobertaServer/src/main/java/de/fhg/iais/roberta/persistence). The entities are found in the `bo` (business objects) sub-directory and are pojos (plain old java objects). The `dao` (data access object) sub-directory contains classes that implement loading and storing entities.

_TODO_:
* main server components

# Web Frontend
The web frontend is written in JavaScript and located in the source tree under [OpenRobertaParent/OpenRobertaServer/staticResources](https://github.com/OpenRoberta/robertalab/tree/develop/OpenRobertaParent/OpenRobertaServer/staticResources).

_TODO_:
* simulation
