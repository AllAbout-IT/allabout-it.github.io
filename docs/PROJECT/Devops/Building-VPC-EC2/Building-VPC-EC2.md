---
layout: default
title: 2.Building VPC, EC2 in AWS
parent: 1.Architecture AWS with Terraform for Automating
grand_parent: PROJECT
# nav_order: 2002
permalink: /docs/PROJECT/Devops/Building-VPC-EC2
---
# Building VPC, EC2 on Console in AWS  
{: .no_toc }

![1](/docs/PROJECT/Devops/Overview/1.png)  

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

---

## Region  

1. click national name text right and top of the window  
![3](/docs/PROJECT/Devops/Building-VPC-EC2/3.png)  

2. Select Region name on the list(Ex> Asia Paciffic(Seoul) ap-northeast-2)  
![4](/docs/PROJECT/Devops/Building-VPC-EC2/4.png)  

## VPC  

### Overview  

This topology's concept is HA(high-available). VPC was built as 10.10.0.0/24 on the ap-northeast-2(Seoul) region. And it was divided from 10.10.10.0/24 to 10.10.40.0/24 into 4 subnets. 2 subnets(10.10.10.0, 10.10.20.0) was selected to 'ap-northeast-2a' and 'ap-northeast-2c' each other as the public subnet. Also, the other 2 subnets were selected to 'ap-northeast-2a' and 'ap-northeast-2c' each other as the private subnet. the public route includes 2 public subnets with an internet gateway. the private route includes 2 private with a nat gateway.  

### VPCs  

1. Type 'VPC' in Serach blank box. and click 'VPC' on the list.  
![2-1](/docs/PROJECT/Devops/Building-VPC-EC2/2-1.png)  

2. Your VPCs > Create VPC
![2-2](/docs/PROJECT/Devops/Building-VPC-EC2/2-2.png)  

3. Select 'VPC only' under 'Resources to create' and put VPC's name you want into blank box under 'Name tag'(ex> dev-pj-vpc)
![2-3](/docs/PROJECT/Devops/Building-VPC-EC2/2-3.png)  

4. Put IPv4 CIDR as B Class into blank box under 'IPv4 CIDR' and let rest of options as defualt, click 'Creat VPC' after done.
![2-4](/docs/PROJECT/Devops/Building-VPC-EC2/5.png)

5. Check VPC's name, status, IPv4 CIDR you made on the VPCs list.
![6](/docs/PROJECT/Devops/Building-VPC-EC2/6.png)  

### Subnets

1. Click 'Creat subnet' after clicking 'Subnets' on the VPC's sidebar.
![7](/docs/PROJECT/Devops/Building-VPC-EC2/7.png)

2. Select VPC you made before by selecting the box under 'VPC ID'.
![8](/docs/PROJECT/Devops/Building-VPC-EC2/8.png)

3. Put the subnet name you want into the blank box under the Subnet name; for example, dev-pub-a-sub.
![9](/docs/PROJECT/Devops/Building-VPC-EC2/9.png)

4. Select the Availability zone where this subnet will reside within the region you selected; for example, ap-northeast-2.  
![10](/docs/PROJECT/Devops/Building-VPC-EC2/10.png)

5. Put the subnet's IPv4 CIDR block into blank box under 'IPv4 CIDR block'. block sizes must be between a /16 netmask and /28 netmask; for example, 10.0.0.0/24.  
![11](/docs/PROJECT/Devops/Building-VPC-EC2/11.png)  

6. Click 'Add new subnet' after done.

7. Make 3 more subnets following below the list as needed from this project.  

	| Subnet name		|	Availabilty zone	|	IPv4 CIDR			|
	|:--------------|:------------------|:--------------|
	|	dev-pub-c-sub	|	ap-northeast-2c		|	10.10.20.0/24	|
	|	dev-pri-a-sub	|	ap-northeast-2a		|	10.10.30.0/24	|
	| dev-pri-c-sub	| ap-northeast-2c		|	10.10.40.0/24	|  

	<!-- ![12-1](/docs/PROJECT/Devops/Building-VPC-EC2/12-1.png) -->
 	<!-- ![12-2](/docs/PROJECT/Devops/Building-VPC-EC2/12-2.png) -->
 	<!-- ![12-3](/docs/PROJECT/Devops/Building-VPC-EC2/12-3.png) -->

8. Click 'Create subnet' after done.  

9. Check system message at top of window and Subnets information(Name, Status, IPv4 CIDR)you made on the list.  
![13](/docs/PROJECT/Devops/Building-VPC-EC2/13.png)  

### Internet Gateway  

\- An internet gateway is a VPC component that enables communication between your VPC and the internet. To use an internet gateway, attach it to your VPC and specify it as a target in your subnet route table.  

1. Click 'Creat internet gateway' in the internat gateway section after clicking 'Internet gateways on ther VPS's left sidebar  
![20](/docs/PROJECT/Devops/Building-VPC-EC2/20.png)  

2. Put internet gateway name into blank box under 'Name tag';for example, dev-igw. and click 'create internet gateway'.
![21](/docs/PROJECT/Devops/Building-VPC-EC2/21.png)

3. Check the message 'The following internet gateway was created [internet gateway ID, name] you can now attach to a VPC to enable the VPC to communicate withe internet.' on the top of the window. so, click 'Attach to a VPC' on the right of message.  
![22](/docs/PROJECT/Devops/Building-VPC-EC2/22.png)

4. Select VPC you made just before on the box under 'Available VPCs' in 'Atttach to VPC section' and click 'Attach Internet gateway'.  
![23](/docs/PROJECT/Devops/Building-VPC-EC2/23.png)

5. Check the message 'Internet gateway [internet gateway ID] successfully attached to [VPC ID] on the top of the window.  
![24](/docs/PROJECT/Devops/Building-VPC-EC2/24.png)

### Nat Gateway  

You can use a network address translation (NAT) gateway to enable instances in a private subnet to connect to services outside your VPC but prevent such external services from initiating a connection with those instances.

A public NAT gateway enables instances in private subnets to connect to the internet but prevents them from receiving unsolicited inbound connections from the internet. You should associate an elastic IP address with a public NAT gateway and attach an internet gateway to the VPC containing it.

1. Click 'Create NAT gateway' in 'NAT gateways' section after clicking 'NAT gateways' on the VPC's sidebar.  
![25](/docs/PROJECT/Devops/Building-VPC-EC2/25.png)  

2. Put NAT gateway name into blank box under 'Name - optional';for example, dev-ngw.  
![26](/docs/PROJECT/Devops/Building-VPC-EC2/26.png)  

3. As you know, NAT gateway have to communicate with out side internet. so, It should be created on public subnet and get public IPv4 address. for this reason, select one of public subnet in the selecting box under 'Subnet'.
![27](/docs/PROJECT/Devops/Building-VPC-EC2/27.png)

4. Select 'Public' in 2 options under 'Connectivity' couse you can recive 'Elastic' IP only when you select 'Public'. and click 'Allocate Elastic IP' after done.
![28](/docs/PROJECT/Devops/Building-VPC-EC2/28.png)

5. Check the message 'Elastic IP address [xxx.xxx.xxx.xxx](Elastic IP's ID) on the top of the window. and check 'Elastic IP allocation ID' that was allocated middle of window.  
![29](/docs/PROJECT/Devops/Building-VPC-EC2/29.png)

6. Click 'Create NAT gateway' after done.
![30](/docs/PROJECT/Devops/Building-VPC-EC2/30.png)

7. Check the message 'NAT gateway [NAT gateway ID]|[NAT gateway name] was create successfully on the top of the window. and check details information. Make sure keep seeing state until it turn from pedding to available and then, check 'Primary public IPv4 address', 'Primary private IPv4 address'.  
![31](/docs/PROJECT/Devops/Building-VPC-EC2/31.png)  

### Route Table  

A route table refers to a table that consists of a set of rules, called routes, that are used to determine where network traffic is directed. In AWS, each subnet in a Virtual Private Cloud (VPC) is associated with a route table, which controls the traffic routing for the subnet. The routes in a route table determine where traffic is directed, either to an Internet gateway, virtual private gateway, Elastic IP address, a VPC endpoint, or another VPC in the same account.

Each VPC has a default route table that controls the traffic routing for all of its subnets. In addition to the default route table, you can create additional custom route tables, which can be associated with one or more subnets in your VPC. This allows you to specify different routing rules for different subnets in your VPC.  

1. Click 'Create route table' on the route tables section after clicking 'Route tables' on the VPS left sidebar.  
![14](/docs/PROJECT/Devops/Building-VPC-EC2/14.png)  

2. Make sure, It needs 2 different route tables in this project. one is a public route table that can communicate with the Internet, and one other is a private route table that It can't communicate from outside the internet.  

3. First of all, put 'route table's name' for the public route table's name into the blank box under 'name - optional'; for example, dev-pub-rt.  
![15](/docs/PROJECT/Devops/Building-VPC-EC2/15.png)

4. Select the VPC you made just before on the box under 'VPC'.
![16](/docs/PROJECT/Devops/Building-VPC-EC2/16.png)  

5. Click 'Create route table' after letting 'Tags' as default.  
![17](/docs/PROJECT/Devops/Building-VPC-EC2/17.png)  

6. Click 'Edit routes' under the detail tab 'Routes' after checking the message 'Route table [route table ID]|[route table name] was created successfully'.
![18](/docs/PROJECT/Devops/Building-VPC-EC2/18.png)  

7. Click 'Add route' on the left down at the Edit route section to add rule in this route table.  
![32](/docs/PROJECT/Devops/Building-VPC-EC2/32.png)  

8. At New 'Edit routes' was expaneded from 'Edit routes', put 0.0.0.0/0 into into blank box under destination. that means 'the target IP or IP range requested from this route table'.
![33](/docs/PROJECT/Devops/Building-VPC-EC2/33.png)

9. Select 'Internet gateway' on the selecting box under 'Target'. and than, It is writ 'igw-...' into box, show igw ID you made just before on the list.  
![34-1](/docs/PROJECT/Devops/Building-VPC-EC2/34-1.png)

10. It shows 'igw-...' on the box with 'igw ID' you made just before on the list. Click your 'internet gateway ID' on the list. and then, click 'save changes'.
![34-2](/docs/PROJECT/Devops/Building-VPC-EC2/34-2.png)

11. Check 'Edit subnet associations' in one of Tap; 'subnet associations' under 'Detail' information box. after checking the message 'Update for route for [route ID]/[route table name] on the top of the window.  
![35](/docs/PROJECT/Devops/Building-VPC-EC2/35.png)  

12. Select 2 public subnets on the 'Available subnets' list because this is for the public route table. and then, click 'Save associations' after done.  
![36](/docs/PROJECT/Devops/Building-VPC-EC2/36.png)  

13. Check the message 'You have successfully updated subnet associations for [route table ID]/[route table name]' on the top of the window. so now we made a public route table that any resource on the public subnets in this route table can communicate with outside internet. also, It can connect to public subnets from outside the internet.  
![37](/docs/PROJECT/Devops/Building-VPC-EC2/37.png)

14. Click 'Create route table' in 'Route tables' section again. from now, you'll make a private route table. it can request from private subnets to outside internet through NAT gateway but, It can't connect from Outside internet to private subnets.  
![38](/docs/PROJECT/Devops/Building-VPC-EC2/38.png)

15. Set information in 'Create table' section as the following next chart.  

|	Create route table|										|
|	Name - optional	 	|	VPC								|
|:------------------|:------------------|
|	dev-pri-tb			 	|	dev-vpc						|

|	Edit route			 |										|
|	Destination			 |	Target						|
|:-----------------|:-------------------|
|	0.0.0.0/0				 | dev-ngw						|

| Edit subnet association|										|
|:-----------------------|:-------------------|
|	Available subnets			 | dev-pri-a-sub			|
|												 | dev-pri-c-sub			|  

## EC2  

Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides scalable computing capacity in the Amazon Web Services (AWS) cloud.

With this, you can launch and manage virtual servers (called instances) in the AWS cloud. Also, you have complete control over the instances you launch and can configure them to meet your needs. EC2 allows you to scale your computing resources up or down, as needed, by adding or removing instances.

Instances are assigned a unique public IP address and can also be assigned a public DNS name, making it easy to connect to them from the Internet.

You can use this to run a wide range of applications and services, including web applications, databases, analytics tools, and big data processing pipelines. These also support a variety of operating systems, so you can run the software you need for your application.  

### Instance  

### Installing Gitlab to Instance  

### AMIs  
