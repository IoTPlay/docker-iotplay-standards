# Notes on RPi & Mac IoTpPlay standards

---> Back to the README file with the [Table of Contents](../README.md).



## The IoTPlay Docker Images

### Currently used Images
|#| Image Used                  |Arm8|x86_64| Source - Link
|-|-----------------------------|----|----- |--------------------------------------------------------------------------|
|1| docker private reg.         | Y  |  N   | todo                                                                     |
|2| docker_nginx_arm            | Y  |  N   | [GitHub IoTPlay](https://github.com/IoTPlay/docker_nginx_arm)            |
|3| docker_mosquitto            | Y  |  Y   | [GitHub IoTPlay](https://github.com/IoTPlay/docker_mosquitto)            |
|4| docker_nodered              | Y  |  Y   | [Docker Hub](https://hub.docker.com/r/nodered/node-red-docker/tags/)     |
|5| docker_mariadb              | Y  |  Y   | [GitHub IoTPlay](https://github.com/IoTPlay/docker-mariadb-alpine)       |
|6| Node-RED HomeKit            | Y  |  Y   | [Docker Hub](https://hub.docker.com/r/raymondmm/node-red-homekit/tags/)  |

### Previously used Images

Previously we had to shape some of our own images, replacements were found. Some lessons learnt in our own.

|#| IoTPlay Image       |Arm8|x86_64| Tgt - Link
|-|----------------------------|----|------|-----------------
|1| docker_nodered IoTPlay     | Y  |  Y   | [GitHub](https://github.com/IoTPlay/docker_nodered)


## Notes on the Images

### Design Principles for IoTPlay Images

1. Use published images - that others maintain. 1st price - if they ar publishes on http://hub.docker.com
2. For `RaspberryPi 2/3's`, As far as possible, docker images are to be built on `arm64v8/alpine`, [link on docker hub](https://hub.docker.com/r/arm64v8/alpine/)
3. Alpine `v3.6`, from `gliderlabs/docker-alpine`, link on [github](https://github.com/gliderlabs/docker-alpine)
4. UserID's of the docker image sometimes clash with the host's's IDs. Some special care is required here. Our Node-RED image is such an example.

### IoTPlay's Images in use
My list of Docker Images, and status below:

|#|IoTPlay Folder    |Tgt Pfrm | O/S   | Base Image                     |Dockerfile           |Status
|-:|---------------- |---------| ----- | -------------------------------|---------------------|------
|1|docker_mariadb    |RPi      |alpine |yobasystems/alpine-mariadb      |--none--             |Prod
|"| "                |Mac      |       |bianjp/mariadb-alpine           |--none--             |Dev
|2|docker_mosquitto  |RPi      |resin  |resin/raspberrypi3-alpine       |Dockerfile_resinPi3  |Prod
|3|docker_nodered    |RPi      |hypriot|hypriot/rpi-node                |Dockerfile_hypriot611|Prod
|"| "                |Mac      |alpine |mhart/alpine-node               |Dockerfile_MacAlpine |Dev
|4|docker_openui5_go |Mac      |alpine |golang:alpine                   |Dockerfile_openui5   |Dev
|5|docker_py_paradox |RPi      |resin  |resin/raspberry-pi-alpine-python|Dockerfile_py_paradox|Test

### About the Base Images

|#| Base Image                      |Version| Notes                       | URL docker hub
|-:|--------------------------------|-------|-----------------------------|-------------
|1|yobasystems/alpine-mariadb       |armhf  | 176MB - too large !!        |[dockerhub](https://hub.docker.com/r/bianjp/mariadb-alpine/)
|2|bianjp/mariadb-alpine            |latest |                             |[github](https://github.com/bianjp/docker-mariadb-alpine)
|3|resin/raspberrypi3-alpine        |3.6    |                             |[dockerhub](https://hub.docker.com/r/resin/raspberrypi3-alpine/)
|4|hypriot/rpi-node                 |6.11   |                             |[dockerhub](https://hub.docker.com/r/hypriot/rpi-node/)
|5|mhart/alpine-node                |9.3.0  |Minimal Node.js Docker Images|[dockerhub](https://hub.docker.com/r/mhart/alpine-node/)
|6|golang:alpine                    |       |Official golang on alpine    |[dockerhub](https://hub.docker.com/_/golang/)
|7|resin/raspberry-pi-alpine-python |latest |Based on resin.io, with Py.  |[dockerhub](https://hub.docker.com/r/resin/raspberry-pi-alpine-python/)


- So, is the chosen image: `resin/raspberry-pi-alpine-node:0.10.22-slim` ???

### What is resin.io ?

resin is used in two images, from the company http://www.resin.io.

Think about moving image 3 - nodered across to alpine + node.js on resin:

- `resin/raspberry-pi-alpine-node`  
  - latest: 457MB !!
  - 0.10.22-slim : 64.6MB

  > This image is part of the resin.io base image series for IoT devices. The image is optimized for use with resin.io and resinOS, but can be used in any Docker environment running on the appropriate architecture.  


- or `resin/raspberrypi3-alpine` ?  for RPi Zero
  - latest : 47.8MB    

  > The bare bones Alpine Linux OS image for Raspberry Pi v1 & ZERO. Maintained by Resin.io.

- for an IoT device: [arm64v8/alpine](https://hub.docker.com/r/arm64v8/alpine/)
  > A minimal Docker image based on Alpine Linux with a complete package index and only 5 MB in size!

### Guidelines to Remember re Other Linux distros vs. Alpine.

1. Alpine does not have useradd, thus use:

```
RUN addgroup -g ${PGID} abc && \
    adduser -D -u ${PUID} -G abc abc

```
2. apt-get does not work on Alpine, see `apk` use here: https://wiki.alpinelinux.org/wiki/Alpine_Linux_package_management


---> Back to the README file with the [Table of Contents](../README.md).
