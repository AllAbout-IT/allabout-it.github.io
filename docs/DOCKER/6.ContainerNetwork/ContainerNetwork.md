---
layout: default
title:  6.Container Network
parent: DOCKER
has_children: true
nav_order: 1006
# permalink: /docs/PROJECT
---

# Container Network

{ :no_toc }

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

## 1. Container Network structure

* Virtual ethernet bridge: 172.17.0.0/16.
* It's based on L2 Layer network.
* The Veth interface is created when the container is created.
* IP within bridge networks are sequential assign while the container running(these will be changed when the container restart).
* The veth interface is created for inside connecting between the 'docker0'bridge and the container. Also, it connects with 'eht0' in the container.
* 'docker0' bonded with the veth interface roled to connect with the eth0 of the host.  
![3](/docs/DOCKER/6.ContainerNetwork/3.png)
![4](/docs/DOCKER/6.ContainerNetwork/4.png)
![5](/docs/DOCKER/6.ContainerNetwork/5.png)

## 2. Port-Forwading  

* It is allowed to connect outside by exposing the container port to out.  
![1](/docs/DOCKER/6.ContainerNetwork/1.png)
* Port exposes through Ipables rule(automatic)  
      1. \-p \<HostPort:ContainerPort>  
      ![2](/docs/DOCKER/6.ContainerNetwork/2.png)  
      2. \-p \<ContainerPort> (Hostport is appointed by random, it can check as 'docker ps')  
      ![6](/docs/DOCKER/6.ContainerNetwork/6.png)
      3. \-P (Specifying the EXPOSE and Random host port specified in the dockerfile, It can check as 'docker ps')  
      ![7](/docs/DOCKER/6.ContainerNetwork/7.png)

## 3. Adding Container network

* The interface network in 'docker0' is not allowed to static mode.
![8](/docs/DOCKER/6.ContainerNetwork/8.png)  
![9](/docs/DOCKER/6.ContainerNetwork/9.png)  

* It is possible to create a user-defined bridge network like docker0. for connecting between eth0 interface in the host and veth interface in the container.
![10](/docs/DOCKER/6.ContainerNetwork/10.png)
![11](/docs/DOCKER/6.ContainerNetwork/11.png)  
![12](/docs/DOCKER/6.ContainerNetwork/12.png)  
  * --driver: You can select network type(bridge, ipvlan, mcvlan, overlay)  
  ![13](/docs/DOCKER/6.ContainerNetwork/13.png)  

  * --subnet: You can designate network range(If you skip it, It'll be applied sequentially from 192.168.100.0)  

  * --gateway: You can designate gateway IP(If you skip it, It'll be applied x.x.x.1 )  

  * mynet: You can create network name you want.  

  * --net: You can designate network that container can using.(If you skip it, It'll be 'docker0')  

  * --ip: You can designate IP that the container can have. (If you skip it, It'll be applied sequentially from x.x.x.1)  

## 4. Container to Container Networking  

* Server & Client service operating by using container
* Sending data whithin appear in container(wordpress) at front area to container(mysql)  
![14](/docs/DOCKER/6.ContainerNetwork/14.png)
![15](/docs/DOCKER/6.ContainerNetwork/15.png)
  * --link: Container connecting setting in same host network  
  * --link \<container name>:\<hosts registered name>  
  * When the link's set up, container information will be registred to 'hosts' file automatically.  
  * If Container's registered IP is changed, hosts information will be modified automatically.
  
  