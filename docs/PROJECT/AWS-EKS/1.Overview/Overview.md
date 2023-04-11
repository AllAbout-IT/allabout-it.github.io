---
layout: default
title: 1.Overview
parent: 2.Architecture AWS with EKS
grand_parent: PROJECT
nav_order: 2001
# permalink: /docs/PROJECT/AWS-EKS/Overview
---
# Architecture AWS with EKS

{ :no_toc }

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

## OVERVIEW  

![1](/docs/PROJECT/AWS-EKS/Overview/pics/1.png)  

## Basic resources in AWS

![2](/docs/PROJECT/AWS-EKS/1.Overview/pics/2.png)

Engineers usually connect to AWS using an IAM user account issued by IAM, rather than a root account. Moreover, it is recommended to use MFA when logging in for added security.

The core infrastructure comprises 2 public subnets and 2 private subnets distributed across availability zones A and C in the AP-Northeast-2 (Korea) region, providing high availability and fault tolerance for the underlying services. Public subnets(10.0.0.0/24, 10.0.1.0/24), Privet subnets(10.0.2.0/24, 10.0.3.0/24), These subnets has a each routing table. Public subnets can communicate with Outside internet through Internet gateway. But, Private subnets can communicate only inside without any gateway.

The subnets are designed with a custom routing configuration, where each subnet is associated with its own routing table. The public subnets (10.0.0.0/24, 10.0.1.0/24) are connected to the Internet Gateway, allowing outbound communication to the Internet. The private subnets (10.0.2.0/24, 10.0.3.0/24) are configured with either a NAT Gateway or a Bastion Host. If a Bastion Host is used, it is created on one of the public subnets to allow outbound Internet communication for services within the private subnet, while inbound traffic is restricted to the internal network only.

Engineers typically access the Bastion Host using SSH key encryption. And use it to access the private subnets to create and manage services. This allows secure access to the private subnets from the Bastion Host instance.

## EKS and Nginx  

![3](/docs/PROJECT/AWS-EKS/1.Overview/pics/3.png)

## EFK(Elastic Search, Fluentd, Kibana) Stack  

![4](/docs/PROJECT/AWS-EKS/1.Overview/pics/4.png)

## Cloudwatch with Slack  

![5](/docs/PROJECT/AWS-EKS/1.Overview/pics/5.png)
