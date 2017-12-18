# jeedom-rpi
A Jeedom Docker image for Raspberry Pi based on Resin Debian and Hypriot mysql images.



This repository contains **Dockerfile** of a dockerized [Jeedom](https://www.jeedom.com) based on a Resin image. The mysql database is based on Hypriot mysql image.


### Base Docker Images

* [hypriot/rpi-mysql](https://hub.docker.com/r/hypriot/rpi-mysql/)
* [resin/armv7hf-debian](https://hub.docker.com/r/resin/armv7hf-debian/)


### Installation

1. Install [Docker](https://www.docker.com/) on your Raspberry pi.

2. Create the directory used to store the mysql database :
```
    mkdir -p /home/pi/jeedom/mysql
```
3. Start a container for the Jeedom database :
```
    docker run --name jeedom-mysql -v /home/pi/jeedom/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=password -e TZ=Europe/Paris -d hypriot/rpi-mysql
```
4. Create the directory used to store the Jeedom data :
```
    mkdir -p /home/pi/jeedom/data
``` 
5. Start a new Jeedom container :
```
    docker run --name jeedom --link jeedom-mysql:mysql --privileged -v /home/pi/jeedom/data:/var/www/html -e ROOT_PASSWORD=jeedom -p 9080:80 -p 9022:22 -d codafog/jeedom-rpi
```
6. Connect to your Raspberry IP at port 9080 with a web browser and enjoy playing with Jeedom.

### Using docker compose

You can also use the docker compose file to build both containers :

1. Run both containers based on the docker-compose.yml file :
```
    docker-compose up
```
### Github

Githud Address : https://github.com/CodaFog/jeedom-rpi
