---
layout: default
title: Setting Workspace
parent: 01.Architecture Application by AWS EKS
grand_parent: AWS Workshop Studio
# great_grand_parent: PROJECT
# has_children: true
nav_order: 1003
# permalink: /docs/01.PROJECT
---
# Setting Workspace

This article is a document from [AWS Workshop studio](https://catalog.us-east-1.prod.workshops.aws/workshops/9c0aa9ab-90a9-44a6-abe1-8dff360ae428/en-US/30-setting) that has been practiced and monitored.

AWS Cloud9 is a cloud-based integrated development environment (IDE) that allows developers to write, run, and debug code from a web browser. It supports a variety of programming languages and can be used to develop various applications, including serverless, web, and mobile applications. Developers can use Cloud9 for code writing, debugging, testing, and deployment.

Cloud9 is integrated with other AWS services such as AWS Lambda, Amazon EC2, and AWS CodeStar, enabling developers to build and deploy applications. It also integrates with collaboration tools such as GitHub and Bitbucket to manage team projects.

As a browser-based IDE, developers can use Cloud9 without installing any software on their local computers. It is cloud-based, so developers do not need to install or maintain software on their computers. They can also leverage AWS security and management features.

## AWS cloud9

### IDE configuration with AWS Cloud9

* Service > Cloud9  
![1](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/03.SettingWorkspace/pics/1.png)

* Click **Create environment** on the AWS cloud9 page  
![2](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/03.SettingWorkspace/pics/2.png)

* Put IDE name in blank box and put description in blank box too. and select **New EC2 instance** at Environment type.  
![3](/docs/02.AwsWorkshopStudio/01.ArchitectAppEKS/03.SettingWorkspace/pics/3.png)

## Create IAM Role

* Select **t3.medium** in instance type at New EC2 instance and select **Amazon Linux(recommended)** in Platform