![Ubooquity Logo](http://i.imgur.com/InPPMtr.png)
=========================================================

[![Docker Stars](https://img.shields.io/docker/stars/zerpex/ubooquity-docker.svg)](https://hub.docker.com/r/zerpex/ubooquity-docker/) [![Docker Pulls](https://img.shields.io/docker/pulls/zerpex/ubooquity-docker.svg)](https://hub.docker.com/r/zerpex/ubooquity-docker/) [![Docker Size](https://img.shields.io/imagelayers/image-size/zerpex/ubooquity-docker/latest.svg)](https://hub.docker.com/r/zerpex/ubooquity-docker/) [![Docker Layers](https://img.shields.io/imagelayers/layers/zerpex/ubooquity-docker/latest.svg)](https://hub.docker.com/r/zerpex/ubooquity-docker/) 

# Introduction

@cromignon has made an image for us in his [own repository](https://github.com/cromigon/ubooquity-docker), but doesn't seems to maintain it anymore.  
This image is built to be as lighweight and simple as possible. It is based on latest alpine and java 8.  

- **Ubooquity version** : 2.0.2

## About Ubooquity

Home server for comics and ebooks

Ubooquity is a free, lightweight and easy-to-use home server for your comics and ebooks. Use it to access your files from anywhere, with a tablet, an e-reader, a phone or a computer.

Main features
* Simple graphical interface to configure your server in a few minutes
* Web administration page available if you prefer to do everything through your browser
* User management with secured access, to decide who can see what
* Online comic reader to read your comics without downloading huge files
* Compatible with Calibre metadata, for better ebooks collection management
* Can be installed on any OS supporting Java (Windows, Linux, Mac OS...) and on a wide range of hardware (desktop computer, server, NAS...)
* Supports many types of files, with a preference for epub, cbz, cbr and PDF files

Copy-pasted from the Ubooquity homepage.

# Getting started

Docker Installation
-------------------
Please see the [Docker installation documentation](https://docs.docker.com/installation/) for details.

## Prerequisite

Ensure that you have folders created for the ubooquity config on the host.
It's generally recommended to have some e-books or comics to mount in :)

## Docker

Run the following command line :

```
docker run --restart=always -d \
  -v /PATH/TO/UBOOQUITY/DATA:/config \
  -v /PATH/TO/COMICSANDBOOKS:/media \
  -p 2202:2202 \
  -p 2502:2502 \
  zerpex/ubooquity-docker
  
```


## Docker-compose

Use the following docker-compose.yml and adapt it to you configuration :

```
ubooquity:
  restart: always
  image: zerpex/ubooquity-docker
  container_name: ubooquity
    - /PATH/TO/UBOOQUITY/CONFIG:/config
    - /PATH/TO/YOUR/COMICS:/media
    - /etc/localtime:/etc/localtime:ro
  environment:
    - TZ=Europe/Paris
  ports:
    - 2202:2202
    - 2502:2502

```

## Notes

Once the container is up:  
- go to http://{YOUR_IP_ADDRESS}:2502/admin and do your configuration according to the [ubooquity documentation](https://vaemendis.github.io/ubooquity-doc/).  
- Then, you can access Ubooquity through http://{YOUR_IP_ADDRESS}:2202
- In order to keep your containers up to date automatically, I recommand you to use [Watchtower](https://github.com/v2tec/watchtower) that will do the job for you :)

# License

Code released under the [MIT license](./LICENSE).
