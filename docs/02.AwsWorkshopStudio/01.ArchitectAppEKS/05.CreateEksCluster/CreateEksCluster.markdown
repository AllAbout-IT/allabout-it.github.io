---
layout: default
title: Create EKS Cluster
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

## Create EKS Cluster with eksctl

### The architecture from now

the architecture of the services configured from now would be creating a Kubernetes cluster with eksctl like below.
![2](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/05.CreateEksCluster/pics/2.png)

### Creating EKS Cluster with eksctl  

If you use eksctl to execute this command (eksctl create cluster) without giving any setting values, the cluster is deployed as a default parameter.

{: .node }
However, we will **create configuration files to customize some values** and deploy it. In later labs, when you create Kubernetes' objects, you create a configuration file that is not just created with the kubectl CLI. This has the advantage of being able to easily identify and manage the desired state of the objects specified by the individual.

* Paste the values below in the root folder(/home/ec2-user/environment) location.

  ```sh
  cd ~/environment
  ```

  ```yml
  cat << EOF > eks-demo-cluster.yaml
  ---
  apiVersion: eksctl.io/v1alpha5
  kind: ClusterConfig

  metadata:
    name: eks-demo # EKS Cluster name
    region: ${AWS_REGION} # Region Code to place EKS Cluster
    version: "1.23"

  vpc:
    cidr: "10.0.0.0/16" # CIDR of VPC for use in EKS Cluster
    nat:
      gateway: HighlyAvailable

  managedNodeGroups:
    - name: node-group # Name of node group in EKS Cluster
      instanceType: m5.large # Instance type for node group
      desiredCapacity: 3 # The number of worker node in EKS Cluster
      volumeSize: 10  # EBS Volume for worker node (unit: GiB)
      privateNetworking: true
      ssh:
        enableSsm: true
      iam:
        withAddonPolicies:
          imageBuilder: true # Add permission for Amazon ECR
          albIngress: true  # Add permission for ALB Ingress
          cloudWatch: true # Add permission for CloudWatch
          autoScaler: true # Add permission Auto Scaling
          ebs: true # Add permission EBS CSI driver

  cloudWatch:
    clusterLogging:
      enableTypes: ["*"]
  EOF
  ```

* If you look at the cluster configuration file, you can define policies through **iam.attachPolicyARNs** and through **iam.withAddonPolicies**, you can also define add-on policies. After the EKS cluster is deployed, you can check the IAM Role of the worker node instance in EC2 console to see added policies.

{: .note}
Click [here](/https://eksctl.io/usage/creating-and-managing-clusters/)  to see the various property values that you can give to the configuration file.

* Using the commands below, deploy the cluster.

  ```sh
  eksctl create cluster -f eks-demo-cluster.yaml
  ```

  ![3](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/05.CreateEksCluster/pics/3.png)

The cluster takes **approximately 15 to 20 minutes** to fully be deployed. You can see the progress of your cluster deployment in AWS Cloud9 terminal and also can see the status of events and resources in AWS CloudFormation console.

* When the deployment is completed, use command below to check that the node is properly deployed.

  ```sh
  kubectl get nodes
  ```


