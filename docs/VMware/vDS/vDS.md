---
layout: default
title: Virtualization Distribute Switch(vDS)
# has_children: true
parent: VMware
permalink: docs/VMware/vDS
---

# Virtualization Distribute Switch(vDS)

{: no_toc }

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

## Definitions

A distributed switch (vDS) is a virtual switch that allows network administrators to manage networking configurations for multiple hosts or virtual machines from a centralized location in a VMware environment. It is a logical switch that spans multiple ESXi hosts and provides advanced networking features that are not available with standard vSwitches. The vDS allows for configuration of networking policies such as traffic shaping, load balancing, and VLANs at the port group level, which are then applied to all connected hosts and virtual machines.
![1](/docs/VMware/vDS/1.png)

## Function

### Centralized management

* The vDS provides a central point of management for all vDS features, allowing administrators to configure the switch itself, create and manage port groups, and monitor network traffic.

### Consistent networking configurations  

* A vDS allows for the creation of consistent networking configurations across multiple hosts and VMs, making it easier to manage and troubleshoot network issues.

### Advanced networking features  

* vDSs provide advanced networking features that are not available with standard vSwitches, such as Network I/O Control (NIOC), which allows for the allocation of network bandwidth to specific traffic types, and support for Link Aggregation Control Protocol (LACP), which provides link aggregation and failover capabilities.  

## LAB-1 Mitration from MGMT(Management) PG(Port Group) to vDW(Virtualzation Distribute Switch)

### Preparing for Working  

![2](/docs/VMware/vDS/2.png)
![3](/docs/VMware/vDS/3.png)
![4](/docs/VMware/vDS/4.png)

### Making vDS  

1. Click New 'Disburite Switch' in 'Distribute Switch' after clicking 'Data Center' under FQDN.
![5](/docs/VMware/vDS/5.png)
![6](/docs/VMware/vDS/6.png)

    New Distributed Switch  
    {: .fs-4 }  
2. Let it be 'DSwith' as name in 'Name and location' Section. and check 'Data Center' as Location, and then, click 'NEXT'.
![7](/docs/VMware/vDS/7.png)
![8](/docs/VMware/vDS/8.png)

3. Select '6.6.0 - ESXi 6.7 and later' as default in 'Select verion' section. and then, click 'NEXT'.  
![9](/docs/VMware/vDS/9.png)  
![10](/docs/VMware/vDS/10.png)  

4. Put '2' into 'Number of uplinks' value box. and select 'Enabled' on the list after clicking 'V' next to 'Network I/O Contro' and Check on the box next to 'Create a default port group'. Put 'DPortGroup' into 'Port group name' value box. and then, click 'NEXT'.  
![11](/docs/VMware/vDS/11.png)  
![12](/docs/VMware/vDS/12.png)  

5. Check the information configured before in the 'Ready to complete' section. And then, click 'FINISH'  
![13](/docs/VMware/vDS/13.png)

6. Click 'DSwitch' in 'Networking' on the left sidebar. and then, Check the topology made from this working after clicking 'Topology' in 'Configure'.  
![14](/docs/VMware/vDS/14.png)

### Adding Hosts to vDS

1. Click 'Add and Manage Hosts' after right clicking on 'DSwitch' in Network on the left sidebar.  
![15](/docs/VMware/vDS/15.png)

    DSwitch - Add and Manage Hosts  
    {: .fs-4 }
2. Select 'Add hosts' in 'Select task' section. And then, click 'NEXT'.  
![16](/docs/VMware/vDS/16.png)

3. Click 'New hosts' in 'Select hosts' section. and then, Click all hosts on the list after appearing new pop-up window 'Select Hosts'. And click 'OK' after done.
![17](/docs/VMware/vDS/17.png)
![18](/docs/VMware/vDS/18.png)

4. Check hosts that are added to the list in 'Select hosts' section after the disappearing pop-up window. And click 'NEXT' after that.  
![20](/docs/VMware/vDS/20.png)
![19](/docs/VMware/vDS/19.png)

5. Select 'vmnic1' connected to 'vSwitch' that was made in this work. And then, click 'Assign uplink' above the list.  
![21](/docs/VMware/vDS/21.png)

6. Select 'uplink 1' on the list in 'Select uplink' pop-up window appeared. And then, click 'OK' after that.  
![22](/docs/VMware/vDS/22.png)
![23](/docs/VMware/vDS/23.png)

7. Assign 'vmnic1' connected to 'ESXi-2(192.168.200.102' to 'Uplink2', as you assigned 'vmnic1' connected to 'ESXi-1(192.168.200.102' to 'Uplink1', which was worked according to Working Steps 5 through 6.  


### Checking Status

## LAB-2 Making vDS for Private Network  

### Preparing for Working  

###
