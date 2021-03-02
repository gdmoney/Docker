## General
```
docker version
docker info										show system-wide info

docker image ls										list images
docker image rm IMAGE_ID					                        delete image
docker image rmi REPO:TAG                                                               delete image

docker run -dit --name ALPINE1 alpine ash						start a container and connect it to the default    bridge
docker run -dit --name ALPINE2 --network ALPINE-NET alpine ash				start a container and connect it to the ALPINE-NET bridge
docker run -dit --name NGINX1  --network TESTBRIDGE -p 8081:80 nginx			start a container, connect it to the TESTBRIDGE and setup port forwarding from 8081 > 80 (host NIC to container)
docker run -dit --name NGINX2  --network TESTBRIDGE -p 8082:80 nginx
docker run -dit --name ALPINE3 --network host alpine ash				start a container and bind it directly to the host's network

docker attach CONTAINER_ID				                                connect to a container
CTRL + pq										disconnect from a container

docker ps										list containers
docker container ls -a

docker container start CONTAINER_ID							start containers
docker container stop  CONTAINER_ID							stop containers
docker container inspect CONTAINER_ID                                                   show detailed info about the container
docker container rm    CONTAINER_ID							delete containers

docker logs CONTAINER_ID                                                                view logs
```


## Networking
```
docker network ls									list networks
docker network create NAME							        create a network
docker network rm     NETWORK_ID							delete a network

docker network inspect host								show detailed info about the host              network
docker network inspect bridge								show detailed info about the default    bridge network
docker network inspect NAME							        show detailed info about the custom bridge network

docker network connect bridge     ALPINE1						connect ALPINE1 container to the default    bridge
docker network connect ALPINE-NET ALPINE2						connect ALPINE2 container to the ALPINE-NET bridge

docker network disconnect ALPINE-NET ALPINE1						disconnect ALPINE1 container from the ALPINE-NET bridge
```


## iptables
```
iptables -L -n -v
iptables -L DOCKER -n -v
iptables -L DOCKER -n -v -t nat
iptables -L DOCKER -n --line-numbers

iptables -A DOCKER -p tcp -s 192.168.255.0/24 -d 172.19.0.2 --dport 80 -j ACCEPT
iptables -A DOCKER -p tcp -s 0.0.0.0/0 -d 172.19.0.2 --dport 80 -j ACCEPT -i net2
iptables -A INPUT -s 0.0.0.0/0 -d 0.0.0.0/0 -j DROP
iptables -I INPUT 12 -p tcp -s 0.0.0.0/0 -d 0.0.0.0/0 --dport 22 -j ACCEPT
iptables -D DOCKER 1							

iptables-save    > /etc/sysconfig/iptables						save new rules to a file
iptables-restore < /etc/sysconfig/iptables						restore new rules from a file
```
