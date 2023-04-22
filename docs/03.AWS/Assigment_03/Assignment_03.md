---
layout: default
title: Assignment_03
parent: AWS
nav_order: 1
---

# Assignment_03_
## 과제: Virtual Private Cloud 생성
이 과제에서는 AMAZONE VPC 마법사를 사용하여 단일 가용영역(AZ)에 인터넷 세이트웨이 1개와 서브넷 2개가 있는 VPC를 생성합니다. 인터넷 세이트웨이는 VPC 구성 요소입니다.

참고: 실습 전체에서 동일한 리전을 사용해야 합니다.  

VPC를 생성한 후 서브넷을 추가할 수 있습니다. 각 서브넷은 하나의 가용 영역 내에 존재하며, 여러 여역에 분산할 수 없습니다. 트래픽이 인터넷 게이트웨이로 라우팅되는 서브넷을 퍼블릭 서브넷이라고 합니다. 서브넷에 인터넷 게이트웨이에 대한 경로가 없는 경우 해당 서브넷을 프라이빗 서브넷이라고 합니다.

또한 마법사는 프라이빗 서브넷의 Amazon EC2 인스턴스에 대한 인터넷 연결을 제공하는 NAT 게이트 웨이를 생성합니다.

마법사를 사용하여 VPC를 프로비저닝하려면 먼저 탄력적 IP 주소를 생성해야 합니다.

탄력적 IP 주소는 동적 클라우드 컴퓨팅을 위해 설계된 라우팅 가능한 고정 퍼블릭 IPv4 주소입니다. 탄력적 IP 주소는 AWS 계정에 할당되며 릴리스할 때까지 할당된 상태로 유지됩니다. 탄력적 IP 주소를 사용하면 주소를 계정의 다른 인스턴스를 가리키도록 도메인에 대한 DNS 레코드에 탄력적 IP 주소를 지정할 수 있습니다.

NAT 게이트웨이를 생성하려면 탄력적 IP 주소가 있어야 합니다. VPC 마법사는 VPC를 생성하는 데 이 주소가 필요합니다.

탄력적 IP 주소는 동적 클라우드 컴퓨팅을 위해 설계된 라우팅 가능한 고정 퍼블릭 IPv4 주소입니다. 탄력적 IP 주소는 AWS 계정에 할당되며 릴리스할 때까지 할당된 상태로 유지됩니다. 탄력적 IP주소를 사용하면 주소를 계정의 다른 인스턴스에 신속하게 다시 매핑하여 인스턴스나 소프트웨어의 오류를 마스킹 할 수 있습니다. 또는 도메인이 인스턴스를 가리키도록 도메인에 대한 DNS 레코드에 탄력적 IP 주소를 지정할 수 있습니다.

NAT 게이트웨이를 생성하려면 탄력적 IP 주소가 있어야 합니다. VPC 마법사는 VPC를 생성하는데 이 주소가 필요합니다.

탄력적 IP주소를 생성하려면 다음을 수행합니다.

4. AWS 관리콘솔의 {Service ⋁} 메뉴에서 EC를 검색하여 선택합니다.
	![][image-1]
5. 왼쪽 탐색 창에서 Network & Security 섹션을 찾아 Elastic IPs를 선택합니다.
	![][image-2]
6. Allocate Elastic IP address 를 선택합니다.
	![][image-3]
7. 화면 맨 아래 ‘Allocate’를 선택합니다.
	![][image-4]  
	![][image-5]

	다음으로, VPC 마법사를 사용하여 VPC를 생성합니다.
8. AWS 관리 콘솔의 Services∨ 메뉴에서 VPC를 검색하여 선택합니다.
	![][image-6]
9. Create VPC 를 선택합니다.
	![][image-7]
10. VPC workflow 를 생성 하기 위하여, Create VPC 페이지의 VPC setting 세션 아래에 다음의 내용으로 구성합니다.  
	중요! 다른 필드는 수정하지 마십시요.
	- Resources to create: VPC, subnets, etc.을 선택합니다.
		![][image-8]

	- Name tag auto-generation 아래: ▢ Auto-generate 선택을 취소합니다.
		![][image-9]

	- Availability Zones (AZs): 1을 선택합니다.
		![][image-10]

	- number of public subnet: 1을 선택합니다.
		![][image-11]

	- Number of private subnets: 1을 선택합니다.
		![][image-12]

	- ▼Customize subnets CIDR block 을 확장
	- Public subnet CIDR block in…: 아래에 10.0.0.0/20 으로 기록된 내용을 10.0.0.0/24로 수정합니다.
		![][image-13]
	- Private subnet CIDR block in… : 아래에 10.0.128.0/20 으로 기록된 내용을 10.0.1.0/24으로 수정합니다.
		1. 
		 

[image-1]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/04.png "4"
[image-2]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/05.png
[image-3]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/06.png
[image-4]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/07.png
[image-5]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/07-1.png
[image-6]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/08.png
[image-7]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/09.png
[image-8]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/10-1.png
[image-9]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/10-2.png
[image-10]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/10-3.png
[image-11]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/10-4.png
[image-12]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/10-5.png
[image-13]:	file:///Users/Junsung/AllAbout-IT.github.io/AllAbout-IT.github.io/docs/2-AWS/903-Assigment_03/10-6.png