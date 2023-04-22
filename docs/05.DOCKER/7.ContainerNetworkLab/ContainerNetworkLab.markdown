---
layout: default
title: 7. Container Network LAB
parent: DOCKER
has_children: true
nav_order: 1007
# permalink: /docs/PROJECT
---
# Container Network LAB  
{:no_toc }

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

## LAB 1. Docker0 network

### Configure containers and networks like below  

![1](/docs/DOCKER/7.ContainerNetworkLab/1.png)

### Required Satisfaction Conditions  

* Container image: busybox:latest
* Connet to inside with creating a container
* CMD ["sh"]
* Check those's IP

#### Buiding Step

* C1  
  $ docker run --name C1 -d -it --rm busybox:latest  
  ![2](/docs/DOCKER/7.ContainerNetworkLab/2.png)
* C2  
  $ docker run --name C2 -d -it --rm busybox:latest  
  ![3](/docs/DOCKER/7.ContainerNetworkLab/3.png)

#### IP check

* C1  
  $ docker attach C1
  / # ifconfig
  ![4](/docs/DOCKER/7.ContainerNetworkLab/4.png)

* C2  
  $ docker attach C2
  / # ifconfig
  ![5](/docs/DOCKER/7.ContainerNetworkLab/5.png)

### Create container with reference to the following conditions

* Container name: web
* Container image: nginx:latest
* Port-forwarding: Port 80  
* Background-Activating  

#### Building step  

* $ docker run -d --name web -p 80:80 nginx:latest  
* -d : background-activating  
* --name: container name
* -p : port-forwarding  
![6](/docs/DOCKER/7.ContainerNetworkLab/6.png)

### Q. How to know container web's IP  

* $ docker inspect web  
![7](/docs/DOCKER/7.ContainerNetworkLab/7.png)
![8](/docs/DOCKER/7.ContainerNetworkLab/8.png)
* You can check docker0's role as a gateway in the container network.

## LAB 2. Port-Forwarding

### O. Run 3 containers by the following below condition.  

* Web1  
      - Container image: nginx:latest
      - Container name: web1  
      - Background-Activating  
      - Insert command : -p 80:80

* Web2  
      - Container image: nginx:latest
      - Container name: web2  
      - Background-Activating  
      - Insert : -p 80  

* Web3  
      - Container image: nginx:latest
      - Container name: web3  
      - Background-Activating  
      - Insert : -P  

### A. Building Step  

* Web1  
      $ docker run --name web1 -d -p 80:80 nginx:latest  
* Web2  
      $ docker run --name web2 -d -p 80 nginx:latest  
* web3  
      $ docker run --name web3 -d -P  
![9](/docs/DOCKER/7.ContainerNetworkLab/9.png)

## LAB 3. Creating User-Defined Network  

### Q. Create a network for use at containers by following the below conditions

* subnet: 192.168.1.0/24  
* gateway: 192.168.1.254  
* network name : cloudnet  

### A. Building step  

        ```
        $ docker network create --driver bridge \
        --subnet 192.168.1.0/24 \
        --gateway 192.168.1.254 \
        ```

![10](/docs/DOCKER/7.ContainerNetworkLab/10.png)

### Check
  
![11](/docs/DOCKER/7.ContainerNetworkLab/11.png)  
