# General ReadMe instructions for iotplay Docker images

These instructions are to drive standardisation between the docker images the Raspberry Pi docker images are built for.

##### Notes on RPi iotplay standards:
- For `RaspberryPi 2/3's`, As far as possible, docker images are to be built on `arm64v8/alpine`, [link on docker hub](https://hub.docker.com/r/arm64v8/alpine/)
- Alpine `v3.6`, from `gliderlabs/docker-alpine`, link on [github](https://github.com/gliderlabs/docker-alpine)

##### Other Linux distros vs. Alpine.

1. Alpine does not have useradd, thus use:

  > ARG PUID  
  > ARG PGID  
  > RUN addgroup -g ${PGID} abc && \
    adduser -D -u ${PUID} -G abc abc  


2. apt-get does not work on Alpine, see `apk` use here: https://wiki.alpinelinux.org/wiki/Alpine_Linux_package_management

## A Readme on the Images that IoTPlay use and experiment with.

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
|1|yobasystems/alpine-mariadb       |armhf  |                             |[dockerhub](https://hub.docker.com/r/bianjp/mariadb-alpine/)
|2|bianjp/mariadb-alpine            |latest |                             |[github](https://github.com/bianjp/docker-mariadb-alpine)
|3|resin/raspberrypi3-alpine        |3.6    |                             |[dockerhub](https://hub.docker.com/r/resin/raspberrypi3-alpine/)
|4|hypriot/rpi-node                 |6.11   |                             |[dockerhub](https://hub.docker.com/r/hypriot/rpi-node/)
|5|mhart/alpine-node                |9.3.0  |Minimal Node.js Docker Images|[dockerhub](https://hub.docker.com/r/mhart/alpine-node/)
|6|golang:alpine                    |       |Official golang on alpine    |[dockerhub](https://hub.docker.com/_/golang/)
|7|resin/raspberry-pi-alpine-python |latest |Based on resin.io, with Py.                      |[dockerhub](https://hub.docker.com/r/resin/raspberry-pi-alpine-python/)


### What is resin.io ?

resin is used in two images, from the company http://www.resin.io.

- Think about moving image 3 - nodered across to alpine + node.js on resin: [reson-rpi-node](resin/raspberry-pi-alpine-node)
