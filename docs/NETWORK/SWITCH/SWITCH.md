---
layout: default
title: SWITCH
# nav_order: 1
parent: NETWORK/SWITCH
---

---
# SWITCH
---
In Cisco networking, a switch is a networking device used to connect devices together and facilitate communication between them. Cisco switches operate at the data link layer of the OSI model, which is responsible for the physical transmission of data.

Physical Structure:
Cisco switches come in a variety of physical sizes and configurations, from small desktop models with a few ports to large chassis-based switches that can accommodate hundreds or thousands of ports. Most Cisco switches have a rectangular box design with multiple ports on the front or back panel. These ports can be connected to other network devices using Ethernet cables.

Functions:
The primary function of a Cisco switch is to direct traffic between devices on the network. When a device sends data to another device, it first sends the data to the switch. The switch then examines the destination MAC address of the data and determines which port the data should be forwarded to, sending it out on that port. This process is known as switching.

Cisco switches also support advanced features such as VLANs, Link Aggregation Control Protocol (LACP), and Quality of Service (QoS). VLANs allow a single switch to be divided into multiple virtual switches, each with its own set of ports and security policies. LACP allows multiple physical links to be combined into a single logical link, providing higher bandwidth and redundancy. QoS allows the switch to prioritize certain types of traffic, such as real-time audio or video, to ensure that they are delivered with minimal delay or loss.

Advantages:
Some advantages of using Cisco switches include:

High performance and reliability: Cisco switches are designed to handle high traffic volumes and provide high levels of uptime and availability.

Advanced features: Cisco switches support a wide range of advanced features, making them suitable for a variety of network configurations.

Scalability: Cisco switches can be easily scaled up or down as the needs of the network change.

Disadvantages:
Some potential disadvantages of using Cisco switches include:

Cost: Cisco switches can be more expensive than switches from other manufacturers, especially for larger or more advanced models.

Complexity: Some of the advanced features of Cisco switches can be complex to configure and manage, requiring specialized knowledge and expertise.

Vendor lock-in: Because Cisco switches are proprietary, they can create a vendor lock-in situation, making it difficult to switch to another vendor's products.

Overall, Cisco switches are a critical component of many modern networks, providing high-speed, low-latency connectivity between devices and supporting a range of advanced features. While they may be more expensive and complex than switches from other vendors, their performance, reliability, and scalability make them a popular choice for many organizations.
1. SWITCH란?  
    - NETWORK에서 말하는 SWITCH란? NETWORK의 확장성을 위해 사용 되는 장비 입니다. BRIDGE도 이와 같은 기능을 하는 모델이지만 하나의 Collison Domain이 인한 확장성의 한계의 대체안으로 나온것이 SWITCH입니다. 가장 큰 차이점은 한개의 Collision Domain을 가지고 있는 Bridge에 반해 Switch은 Port당 Collision Domaind을 가지고 있어 고성능 네트워크에 사용되고 있습니다. 자세한 Bridge에 관한 내용은 따로 자세하게 다루겠습니다.
<br>
2. SWITCH와 BRIDGE의 차이점?
    - SWITCH와 BRIDGE의 차이점이란 사용할수 있는 Collision의 수, 이름, 선호도 정도 입니다. 사람들이 장비를 구매할떄 많이 혼동하는 이유이기도 합니다. 하지만, 이 둘은 기술적으로는 아주 중요한 차이를 가지고 있습니다.

    - 첫번째는 Bridge는 소프트웨어즉 논리적으로 프레임 정보를 처리하지만 Swtich는 bridge의 처리 방식을 하드웨어(ASIC-Application-Specific-Intergrated-Circuit)로 하기때문에 처리속도가 상대적으로 훨씬 더 빠릅니다.

    - 두번째 bridge는 모든 포트들이 같은 속도를 가지지만 Switch는 속도가 다른 포트를 서로 연결할수 있게 합니다.

    - 세번째 확장성의 범위의 차이입니다. Bridge는 2 ~ 3개의 port들만 있는 반면 Switch는 기본적으로는 수십개 부터 모델에 따라서 많개는 몇백개 까지 연결이 가능합니다.

    - 네번째, Switch는 Cut-through, 또는 Store-and-forwad 방식을 사용하는 데 비해서 Bridge 는 오직 Store-and-forwad 방법만을 사용합니다.  

      1. Store-and-foward는 입력되는 프레임을 먼저 받은 뒤 요청받은 정보를 처리하는 방식입니다.  
      2. Cut-through는 프레임의 목적지 주소만 본 후 바로 전송 처리를 시작하는 방식입니다. 앞선 언급한 Store-and-foward보다 처리속도는 빠르지만 오류의 해결에는 약점을 가지고 있습니다.  


2. SWITCH의 기능  <br><br>
  2.1 Switch는 Bridge와 기능이 같습니다.
