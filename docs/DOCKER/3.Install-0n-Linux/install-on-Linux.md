---
layout: default
title:  Install Docker Engine on Ubuntu
parent: DOCKER
has_children: true
nav_order: 1003
# permalink: /docs/PROJECT
---

# Install Docker Engine on Ubuntu

{ :no_toc }

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

* This script is written as of March 6, 23  
* If you want to know more about installation docker engine in ubuntu, click below.  
[docs.docker.com](https://docs.docker.com/)

## TOPOLOGY

![1](/docs/DOCKER/Install-0n-Linux/1.png)

## Confugure goal

* Common
      - CPU: 2 proccessor
      - RAM: 4GB
      - Storage: 20GB
      - Demon: openssh-server, curl, vim, docker
      - Default.target: GUI > TUI  
      - Hosts:  
              master  10.13.0.101
              node1   10.13.0.102
              node2   10.13.0.103

* K8S-Master  
      - OS: Ubuntu 20.04
      - Machine Name: K8E-master  
      - User: student/ Password: Vmware1!  
      - Hostname: master  
      - Network: Manual/ K8E-Master/ 10.13.0.101  
      - DNS: Manual/ 8.8.8.8  

* K8S-Node1  
      - OS: Ubuntu 22.04
      - Machine Name: K8E-Node1  
      - User: student/ Password: Vmware1!  
      - Hostname: node1  
      - Network: Manual/ K8E-Master/ 10.13.0.102  
      - DNS: Manual/ 8.8.8.8  

* K8E-Node2  
      - OS: Ubuntu 22.04
      - Machine Name: K8E-Node2  
      - User: student/ Password: Vmware1!  
      - Hostname: node2  
      - Network: Manual/ K8E-Master/ 10.13.0.103  
      - DNS: Manual/ 8.8.8.8  
  
## Network Configure in VMware  

1. VMware > Settings > Network
![2](/docs/DOCKER/Install-0n-Linux/2.png)  

2. Click the lock to make changes and put '+' box for adding custom network  
![3](/docs/DOCKER/Install-0n-Linux/3.png)  

3. When a new 'vmnet' appear on the list, change the name to 'K8E-Master' after left double click. and set up the detail option like next.  
![4](/docs/DOCKER/Install-0n-Linux/4.png)  

4. Close pop-up window  
  
## Install Ubuntu 20.04 on VMware  

1. Download Ubuntu ISO iamge for installing at [here](https://releases.ubuntu.com/focal/)  
![5](/docs/DOCKER/Install-0n-Linux/5.png)  

2. VMware > NEW or Virtual Machine
![6](/docs/DOCKER/Install-0n-Linux/6.png)  
![6-1](/docs/DOCKER/Install-0n-Linux/6-1.png)

3. Double left-click on the box that writes 'install from disc of image' on top of the window.
![7](/docs/DOCKER/Install-0n-Linux/7.png)

4. You can drag iso image you want into window or select it after clicking the box that writes 'Use another disc image' bottom of the window. and then, click 'Go back' after done.
![8](/docs/DOCKER/Install-0n-Linux/8.png)

5. If the image you want loads on the window, click the image block so that you can click 'Continue' right bottom of the window.
![9](/docs/DOCKER/Install-0n-Linux/9.png)

6. uncheck to 'Easy to install' and then, click 'Continue'.
![10](/docs/DOCKER/Install-0n-Linux/10.png)

7. Check 'Specify the boot firmware' option that selected to 'Legacy BIOS'. and then click 'Continue'  
![11](/docs/DOCKER/Install-0n-Linux/11.png)

8. 