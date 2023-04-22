---
layout: default
title: Cluster
# has_children: true
parent: vSphere
grandparent: VMware
# permalink: docs/VMware/Cluster
---

# Cluster
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

A DRS (Distributed Resource Scheduler) cluster is a group of virtual machines (VMs) and hosts managed by VMware vSphere's DRS technology. This cluster allows the vSphere environment to automatically balance VM workloads across the hosts in the cluster, based on resource usage, policies, and requirements.  

## Structure  

A DRS cluster consists of two or more physical hosts, each running VMware vSphere. These hosts are connected to shared storage, allowing VMs to be moved between hosts without disrupting their storage. The hosts and VMs in the cluster are managed by a single vCenter Server instance, which controls the allocation of resources and the movement of VMs between hosts.
![1](/docs/VMware/DRS_Cluster/1.jpg)  
Image from [VMware](https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.vmware.com%2Fproducts%2Fvsphere%2Fdrs-dpm.html&psig=AOvVaw3kTRqZw8IjBba545v1IhIV&ust=1677567011563000&source=images&cd=vfe&ved=0CBEQjhxqFwoTCODimqCOtf0CFQAAAAAdAAAAABAQ)

## Function  

DRS technology continuously monitors resource utilization across hosts in the cluster and automatically migrates VMs to other hosts with more available resources as needed, ensuring that VMs have access to the resources they need to run optimally. DRS also optimizes the placement of new VMs, taking into account the requirements of the VM and the resources available on each host. By optimizing VM placement and load balancing, DRS helps to improve performance, reduce downtime, and maximize the utilization of the virtual infrastructure.  
<!-- ![2](/docs/VMware/DRS_Cluster/2.png)   -->

## Strenghts

### Dynamic resource allocation  

DRS enables dynamic allocation of resources across the cluster, ensuring that VMs have access to the resources they need to run efficiently.

### Load balancing

DRS continuously balances the load across hosts, preventing resource bottlenecks and improving performance.

### Automations  

DRS automates resource allocation and VM placement, reducing the need for manual intervention and increasing efficiency.  

### High availability  

DRS helps to ensure high availability by automatically migrating VMs to other hosts in the event of a host failure or maintenance.

### Scalability  

DRS allows organizations to easily scale their virtual infrastructure as needed, adding new hosts and VMs to the cluster as required.  

## Weaknesses

### Complexity  

DRS can be complex to set up and configure, requiring a deep understanding of the vSphere environment and DRS technology.

### Overhead

DRS requires additional resources to operate, including CPU cycles and network bandwidth.  

### Cost  

DRS is only available in VMware's more expensive vSphere editions, which can be a significant cost for smaller organizations or those with limited budgets.

### Dependency on Center  

DRS relies on vCenter Server to function, which can be a single point of failure if not properly configured or maintained.

## LAB-01. Creating a vCluster

### Preparing for Working  

![3](/docs/VMware/DRS_Cluster/3.png)

### Creating a Cluster  

1. 

### Configuration a Cluster  

## LAB-02. Configuration for HA(High Available)  


