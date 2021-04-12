[![CI](https://github.com/orbitalteapot/youtube-pi-image-gen/actions/workflows/build.yml/badge.svg)](https://github.com/orbitalteapot/youtube-pi-image-gen/actions/workflows/build.yml)
# PI Image Generator
Generate images using:
- Docker for linux on ubuntu:20.10 or debian:buster
- Docker for windows with WSL2 kernel

## Prerequisite
- Docker
- Docker-compose

## Build images using docker-compose
### Modify ENV
Configure docker-compose.yml after your need
```yml
USE_QCOW2: 0
BASE_QCOW2_SIZE: "12G"
IMG_NAME: Orbital-Image
RELEASE: buster
LOCALE_DEFAULT: en_GB.UTF-8
TARGET_HOSTNAME: orbitalteapot
KEYBOARD_KEYMAP: "gb"
KEYBOARD_LAYOUT: "English (UK)"
TIMEZONE_DEFAULT: UTC
FIRST_USER_NAME: yourusername
FIRST_USER_PASS: supersecretpassword
WPA_ESSID: yourssid
WPA_PASSWORD: yourwifipassword
WPA_COUNTRY: gb
ENABLE_SSH: 1 # 0 or 1
PUBKEY_SSH_FIRST_USER: ""
PUBKEY_ONLY_SSH: 0 # 0 or 1
STAGE_LIST: stage* # Define stages you want to run
```

### Image output
You have to replace username with your own and create the deploy folder
```yml
    volumes: 
    - type: bind
      source: /home/username/deploy/ # Your pi images will end up here
      target: /build/pi-gen/deploy/
```


To build the image run
```sh
docker-compose up
```
## Build images using docker
If you use this method you can copy the images with docker cp, or add a volume bind to the command.

Renember to edit the env.list with your configuration.
```sh
docker pull ghcr.io/orbitalteapot/youtube-pi-image-gen:latest
docker run --privileged --name orbitalteapotbuild -it --env-file /mnt/d/youtube-pi-image-gen/debian/env.list ghcr.io/orbitalteapot/youtube-pi-image-gen ./startup.sh
docker cp orbitalteapotbuild:/build/pi-gen/deploy /home/yourusername/deploy
```

## Refrence Documentation
This tutorial is using the pi-gen project on github
- The pi-gen [repo](https://github.com/RPi-Distro/pi-gen)
- Install docker for [windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)
- Install docker for [linux](https://docs.docker.com/engine/install/)

