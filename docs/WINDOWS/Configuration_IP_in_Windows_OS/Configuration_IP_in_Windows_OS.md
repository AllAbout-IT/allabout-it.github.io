---
layout: default
title: Configuration IP in Windows OS
nav_order: 103
parent: WINDOWS
style: Heading style (string, default consistent, values atx / atx_closed / consistent / setext / setext_with_atx / setext_with_atx_closed
---

# Configuration IP in Windows OS  

## Open the Network Connections Tool

1. ### Use the Run Command Dialog Box  

    1. Press Win + R to run command dialog box  
    ```[Windows key] + R```
    2. Type 'ncpa.cpl' and press Enter to open the Network Connection tool  
    ![1-2](/docs/WINDOWS/Configuration_IP_in_Windows_OS/1-2.png)  

2. ### In toolbar

    1. Click Network Icon In toolbar  
    ![2-1](/docs/WINDOWS/Configuration_IP_in_Windows_OS/2-1.png)
    2. Click Network you're using now.  
    ![2-2](/docs/WINDOWS/Configuration_IP_in_Windows_OS/2-2.png)
    3. Click 'Change adapter options' at Settings > Ethernet in new pop-up window.  
    ![2-3](/docs/WINDOWS/Configuration_IP_in_Windows_OS/2-3.png)  

3. ### in Quick Access Menu  

    1. Press [Windows key] + [Shift] + x  
    ![3-1](/docs/WINDOWS/Configuration_IP_in_Windows_OS/3-1.png)
    2. Click 'Network Connections' on Quick Access Menu  
    ![3-2](/docs/WINDOWS/Configuration_IP_in_Windows_OS/3-2.png)

## Open Internet Protocol Version 4 (TCP/IPv4) Properties  

1. Click Ethernet0 in Network Connections  
![4-1](/docs/WINDOWS/Configuration_IP_in_Windows_OS/4-1.png)  
2. Click 'Properties' on Ethernet0 Status po-up window  
![4-2](/docs/WINDOWS/Configuration_IP_in_Windows_OS/4-2.png)  
3. Double click 'Internet Protocol Version 4(TCP/IPv4)' on Ethernet0 Properties > Networking > This connection uses the following items:  
![4-3](/docs/WINDOWS/Configuration_IP_in_Windows_OS/4-3.png)  

## Configure IP  

1. Obtain an IP address automatically  
\- It can revice IP address automatically from DHCP  
![5-1](/docs/WINDOWS/Configuration_IP_in_Windows_OS/5-1.png)
2. Use the following IP address  
\- you can filled manual version 4 ip information in this section  
![5-2](/docs/WINDOWS/Configuration_IP_in_Windows_OS/5-2.png)
    * IP address: xxx.xxx.xxx.xxx  
    \- ex> 192.168.102.10  
    ![5-3](/docs/WINDOWS/Configuration_IP_in_Windows_OS/5-3.png)  
    * Subnet mask : xxx.xxx.xxx.xxx  
    \- ex> 255.255.255.0 (/24)  
    ![5-4](/docs/WINDOWS/Configuration_IP_in_Windows_OS/5-4.png)  
    * Default Gateway  
    \- ex> 192.168.102.254  
    ![5-5](/docs/WINDOWS/Configuration_IP_in_Windows_OS/5-5.png)
3. Obtain DNS server address automatically  
\- It can revice DNS IP address automatically from DHCP  
![5-6](/docs/WINDOWS/Configuration_IP_in_Windows_OS/5-6.png)
4. Use the following DNS server addresses  
\- you can filled DNS IP addresses in this section  
![5-7](/docs/WINDOWS/Configuration_IP_in_Windows_OS/5-7.png)
