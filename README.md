Docker Images
=============

This repository contains docker images for:

* JBoss EAP
* Jenkins Base
* Sonatype Nexus
* SonarQube
* NodeJS

Instructions
=============
Build a docker image

```
$ cd [image_name]
$ docker build -t [image_name] .
```

Start a docker container in detached mode
```
$ docker run -d -P [image_name]
```
