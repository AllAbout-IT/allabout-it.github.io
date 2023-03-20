---
layout: default
title: LAB_Build WEB, FTP, DNS, DHCP
nav_order: 102
parent: WINDOWS
---
LAB_Build WEB, FTP, DNS, DHCP
====

1. 구성목표
윈도우서버에 WEB, FTP, DNS, DHCP 서버를 구축하고 작동을 확인.  

2. 사전구성
    * Server1  
    \-  Windows Server 2016(GUI)
    \-  Computer name: FIRST  
    \-  IP: 192.168.111.10(STATIC)
    * Server2
    \-  Windows Server 2016(GUI)
    \-  Computer name: SECOND  
    \-  IP: 192.168.111.20(STATIC)
    * Client1
    \- Windows 10(GUI)
    \- Computer name: Client_1
    \- IP: DHCP
    * Client2
    \- Windows 10(GUI)
    \- Computer name: Client_2
    \- IP: DHCP

3. 구축  
    * STEP1. (First Server에 DHCP구성)  
      - DHCP 설치  
          1. Server Manager 구동
          ![3-1](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-1.png)
          2. Manage > Add Role and Features  
          ![3-2](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-2.png)  
          3. 새로운 팝업창에서 Server Selection 클릭 후 Server Role 클릭 
          \- Server Selection을 클릭해야 Server Role 선택 가능
          ![3-3](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-3.png)  
          4. Server Role List에서 'DHCP Server'체크  
          ![3-4](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-4.png)  
          5. 새로운 Pop-up 창에서 설치할 서비스를 확인하고 'Add Feartures' 클릭
          ![3-5](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-5.png)  
          6. NEXT  
          ![3-6](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-6.png)  
          7. Features에서 NET Framework 설치 확인
          ![3-7](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-7.png)  
          - 만약 설치가 되어 있지 않다면 NET Framework를 먼저 설치 한 후에 DHCP서버를 설치하자.  
          8. NEXT > NEXT > INSTALL  
          ![3-8](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-8.png)  
          9. INSTALL 완료 확인 후 Close 클릭  
          ![3-9](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-9.png)      
      - DHCP Configuration  
          1. Server manager > Tools > DHCP 클릭  
          ![3-10](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-10.png)
          2. DHCP > [Computer Name] > IPv4 에서 우클릭  
          ![3-11](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-11.png)  
          3. 목록에서 'New Scope...' 선택  
          ![3-12](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-12.png)  
          4. 새 팝업창에서 작업을 위해 'Next'  
          ![3-13](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-13.png)
          5. Scope Name 섹션에서 Name에 임의의 이름을 지정 이번 예제에서는 'VLAN 111'로 지정
          ![3-14](/docs/WINDOWS/LAB_WEB_FTP_DNS_DHCP/3-14.png)
          6. IP Address Range에서는 DHCP가 IP를 제공하는 영역을 설정한다. Start IP address에는 영역의 시작 IP를, End IP address에는 영역의 마지막 IP를 입력한다.
          Propagate에서는 제공되는 network의 


    GW : 192.168.111.254
    DNS : 192.168.111.100
    SECOND Server는 192.168.111.200을 할당받도록 구성합니다.
    WIN10-1은 임의의 IP를 할당받도록 구성합니다.
  
  STEP2.  (FIRST Server에 DNS구성)
    - Domain Name: this.com으로 구성합니다.
    - THIS.COM의 FTP Server는 ftp.this.com으로 구성(192.168.111.200)

  STEP3. (SECOND Server를 WEB, FTP구성)
    - IIS를 구성하고, WEB Service를 구성합니다. WEB 초기 페이지는 "THIS.COM을 SECOND Server입니다."로 구성합니다.
    - FTP Service를 구성합니다. FTP를 구성합니다. (익명연결로 구성합니다.)

    확인1. WIN10-1에서 www.this.com으로 접속이 되는 것을 확인합니다.
    확인2. WIN10-1에서 ftp를 이용하여, ftp.this.com으로 접속이 되고 파일이 다운로드 되는 것을 확인합니다. 
