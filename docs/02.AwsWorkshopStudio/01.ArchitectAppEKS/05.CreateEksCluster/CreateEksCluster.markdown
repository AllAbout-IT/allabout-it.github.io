---
layout: default
title: 05. Create EKS Cluster
parent: 01.Architecture Application by AWS EKS
grand_parent: AWS Workshop Studio
# great_grand_parent: PROJECT
# has_children: true
nav_order: 1005
# permalink: /docs/01.PROJECT
---
# Create EKS Cluster

{ :no_toc }

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

Amazon EKS clusters can be deployed in various ways.

* Deploy by clicking on [**AWS console**](/https://console.aws.amazon.com/eks/home#/)

* Deploy by using IaC(Infrastructure as Code) tool such as [**AWS CloudFormation**](/<https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)> or [**AWS CDK**](/https://docs.aws.amazon.com/cdk/api/latest/)

* Deploy by using [eksctl](/https://eksctl.io/)

* Deploy to Terraform, Pulumi, Rancher, etc.

![1](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/05.CreateEksCluster/pics/1.png)

In this lab, we will create an EKS cluster using **eksctl**.

## 