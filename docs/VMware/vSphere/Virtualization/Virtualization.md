---
layout: default
title: Virtualization
# nav_order: 100
# has_children: true
parent: vSphere
grandparent: VMware
#permalink: docs/VMware/Virtualization
---

# Virtualization
{: no_toc }

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

## Definition  

Virtualization is a technology that enables the creation of virtual versions of physical resources such as servers, storage devices, and networks. In IT, virtualization has revolutionized the way organizations operate their IT infrastructure by providing numerous benefits such as increased efficiency, flexibility, scalability, and cost savings.  
![1](/docs/VMware/Virtualization/1.png)

## Benefits of Using Virtualization

### Increased efficiency  

By running multiple virtual machines on a single physical server, virtualization increases server utilization and reduces hardware costs.

### Flexibility  

Virtualization enables organizations to easily allocate and reallocate resources, such as storage and processing power, as needed.

### Scalability  

Virtualization allows organizations to quickly and easily scale their IT infrastructure to meet changing demands.

### Disaster recovery and business continuity  

Virtualization enables organizations to quickly restore operations in the event of a disaster, as virtual machines can be easily moved to another location.

### Improved security  

Virtualization allows organizations to isolate applications and data, reducing the risk of a security breach.  

### Virtual machine encapsulation  

It is a key concept in VMware virtualization technology. It is achieved through a hypervisor, a piece of software that runs on the physical server and manages the virtual machines. The hypervisor provides a virtualized environment for each virtual machine, allocating resources and ensuring that each virtual machine has the resources it needs to run effectively.

Virtual machine encapsulation also provides a layer of security, as each virtual machine is isolated from the others and from the underlying physical hardware. This helps to prevent potential security breaches and protect sensitive data.
![6](/docs/VMware/Virtualization/6.jpg)

## Types of virtualization

### CPU virtualization  

It's a critical component of VMware's virtualization technology, providing the foundation for running multiple virtual machines on a single physical server. It enables organizations to better utilize their hardware resources, reduce costs, and improve the efficiency of their IT infrastructure.
![5](/docs/VMware/Virtualization/5.png)

### Server virtualization  

This involves creating virtual servers on a single physical server, allowing multiple operating systems to run on the same hardware. This increases server utilization and reduces hardware costs.

### Storage virtualization  

This technology abstracts physical storage from the servers that access it, allowing administrators to manage storage as a single pool of resources.
![2](/docs/VMware/Virtualization/2.png)

### Network virtualization  

This involves creating virtual networks on top of a physical network infrastructure. This allows for the creation of isolated network environments for different applications and departments.  
![3](/docs/VMware/Virtualization/3.png)

### Desktop virtualization  

This involves creating virtual desktops that users can access from anywhere, on any device. This enables organizations to centralize desktop management and provides users with a consistent experience, regardless of the device they use.
![4](/docs/VMware/Virtualization/4.jpg)

## The difference between a Physical Machine and a Virtual Machine

### Physical machine

* A physical machine is a physical computer that runs on physical hardware.  
* It has its own operating system, storage, and other hardware components.  
* Those are typically dedicated to running a single application or operating system.

### Virtual machine  

* This is a software-based emulation of a physical machine.  
* It runs on top of a host operating system and has its own virtualized operating system, storage, and hardware components.  
* Multiple virtual machines can run on a single physical machine, sharing the physical resources of the host machine.  

### Resource allocation  

* In a physical machine, the hardware resources are dedicated to the machine and cannot be shared with other physical machines.  
* In a virtual machine, the virtualized hardware resources are dynamically allocated by the virtualization software, allowing multiple virtual machines to share the resources of a single physical machine.

### Portability  

* Physical machines are tied to the physical hardware on which they run and cannot easily be moved from one machine to another.  
* Virtual machines, on the other hand, can be easily moved between physical machines or stored as files for later use.

### Maintenance  

* Physical machines require regular maintenance and upgrades to keep them running smoothly.  
* Virtual machines can be maintained and upgraded more easily, as the virtualization software can take care of many of these tasks automatically.

### Cost  

* Physical machines can be more expensive to purchase and maintain than virtual machines, as they require dedicated hardware and software components.  
* Virtual machines are typically less expensive, as they can run on less expensive hardware and share resources with other virtual machines.
