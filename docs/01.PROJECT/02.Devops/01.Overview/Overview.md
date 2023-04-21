---
layout: default
title: Overview
parent: 02.Architecture AWS with Terraform for Automating
grand_parent: PROJECT
# nav_order: 2001
# permalink: /docs/01.PROJECT/02.Devops/01.Overview
---
# Architecture AWS with Terraform for Automating
{ :no_toc }

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

## Overview  

This 01.PROJECT is about Architecture AWS, Terraform for Automating. It will be described how to build VPC, EC2, ECS, Lambda, Bridge Event, Cloud Watch at AWS. in addition, It will describe how to write and run about terraform to automate operating AWS and build several tools for it.  

## Building VPC, EC2 in AWS  

It will be composed Network, Subnet, Route with Internet Gateway, Nat Gateway in VPC and Instance in EC2.  

![1](/docs/01.PROJECT/02.Devops/01.Overview/1.png)  

## Buiding Load balancer and ECS  

This section will be composed of a Load balancer, a Target group for operating ECS and Cluster, Task Definition, Service in ECS.  

![2](/docs/01.PROJECT/02.Devops/01.Overview/2.png)

## Making boto3 script on python for automating Lamda in AWS  

This section would be processing making a python script using boto3 for operating AWS resources. also, it could be running with the lambda and the bridge event. and we can check every process through the cloud watch.  

![3](/docs/01.PROJECT/02.Devops/01.Overview/3.png)  

## Making terraform script for buiding AWS resources  

This section would be processing making a Terraform script through Terraform Cloud. First of all, the environment that was built can support syncing the local, cloud, private sources in AWS. It can sync to GitLab in EC2 Instance. and This script resources can provide AWS resources.  

![4](/docs/01.PROJECT/02.Devops/01.Overview/4.png)
