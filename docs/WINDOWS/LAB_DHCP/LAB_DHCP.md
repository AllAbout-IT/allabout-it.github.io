---
layout: default
title: LAB_Build DHCP
nav_order: 101
parent: WINDOWS
---

# LAB_Build DHCP  


1. 구성목표
윈도우서버에 DHCP 서버를 구축하고 작동을 확인.  

2. 사전설정  

    * Vmware DHCP 기능 해제 (MAC용 Vmware Fusion12기준)  
      1. Vmware > Settings  
      ![2-1](/docs/WINDOWS/LAB_DHCP/2-1.png)  

      2. Network > Custom to my Mac 에서 구축에 사용할 네트워크 선택  
      ![2-2](/docs/WINDOWS/LAB_DHCP/2-2.png)  

      3. 설정 섹션에서 구축에 사용할 Network를 확인한뒤 'Provide addresses on this network via DHCP'의 체크박스를 해제  
      ![2-3](/docs/WINDOWS/LAB_DHCP/2-3.png)  

    * Server and Computers  

      1. Server 1  
          * Windows Server 2016(GUI)  
          * Computer name: FIRST  
          [윈도우에서 컴퓨터 이름 지정](https://allabout-it.github.io/docs/WINDOWS/How_to_change_your_computers_name/How_to_change_your_computers_name/)  
          ![2-4](/docs/WINDOWS/LAB_DHCP/2-4.png)  
          * IP: 192.168.102.10(STATIC)  
          ![2-5](/docs/WINDOWS/LAB_DHCP/2-5.png)  
          [윈도우OS GUI에서 IP확인 및 설정 방법](https://allabout-it.github.io/docs/WINDOWS/Configuration_IP_in_Windows_OS/Configuration_IP_in_Windows_OS/)  

      2. Client1
          * Windows 10(GUI)
          * Computer name: Client_1
          * Subnet IP: 192.168.102.0(Vmware Network Adapter)  
          * IP: DHCP  

      3. Client2
          * Windows 10(GUI)
          * Computer name: Client_2
          * Subnet IP: 192.168.102.0(Vmware Network Adapter)  
          * IP: DHCP  


4. 구축  

    * STEP1. (First Server에 DHCP구성)

      - DHCP 설치  

          1. Server Manager 구동
          ![3-1](/docs/WINDOWS/LAB_DHCP/3-1.png)  

          2. Manage > Add Role and Features  
          ![3-2](/docs/WINDOWS/LAB_DHCP/3-2.png)  

          3. 새로운 팝업창에서 Server Selection 클릭 후 Server Role 클릭 
          \- Server Selection을 클릭해야 Server Role 선택 가능  
          ![3-3](/docs/WINDOWS/LAB_DHCP/3-3.png)  

          4. Server Role List에서 'DHCP Server'체크  
          ![3-4](/docs/WINDOWS/LAB_DHCP/3-4.png)  

          5. 새로운 Pop-up 창에서 설치할 서비스를 확인하고 'Add Feartures' 클릭.  
          ![3-5](/docs/WINDOWS/LAB_DHCP/3-5.png)  

          6. NEXT  
          ![3-6](/docs/WINDOWS/LAB_DHCP/3-6.png)  

          7. Features에서 NET Framework 설치 확인
          ![3-7](/docs/WINDOWS/LAB_DHCP/3-7.png)  
          \- 만약 설치가 되어 있지 않다면 NET Framework를 먼저 설치 한 후에 DHCP서버를 설치하자.  

          8. NEXT > NEXT > INSTALL  
          ![3-8](/docs/WINDOWS/LAB_DHCP/3-8.png)  

          9. INSTALL 완료 확인 후 Close 클릭  
          ![3-9](/docs/WINDOWS/LAB_DHCP/3-9.png)  

      - DHCP Configuration  

          1. Server manager > Tools > DHCP 클릭  
          ![3-10](/docs/WINDOWS/LAB_DHCP/3-10.png)  

          2. DHCP > [Computer Name] > IPv4 에서 우클릭  
          ![3-11](/docs/WINDOWS/LAB_DHCP/3-11.png)  

          3. 목록에서 'New Scope...' 선택  
          ![3-12](/docs/WINDOWS/LAB_DHCP/3-12.png)  

          4. 새 팝업창에서 작업을 위해 'Next'  
          ![3-13](/docs/WINDOWS/LAB_DHCP/3-13.png)  

          5. Scope Name 섹션에서 Name에 임의의 이름을 지정 이번 예제에서는 'VLAN 102'로 지정  
          ![3-14](/docs/WINDOWS/LAB_DHCP/3-14.png)  

          6. IP Address Range에서는 DHCP가 IP를 제공하는 영역을 설정한다. Start IP address에는 영역의 시작 IP를, End IP address에는 영역의 마지막 IP를 입력한다. Propagate에서는 제공되는 network의 범위를 지정한다. 설정을 마치고 'NEXT'.
          ![3-15](/docs/WINDOWS/LAB_DHCP/3-15.png)  

          7. Add Exclusions and Delay는 DHCP를 제공하지 않는 범위를 선택할 수 있다. 없다면, 'NEXT'
          ![3-16](/docs/WINDOWS/LAB_DHCP/3-16.png)  

          8. 'Lease Duration'에서는 IP 임대 기간을 설정할수가 있다. 기기의 목적에 따라 임대 시간을 '일', '분', '초' 단위로 적절히 부여할 수 있다. 특별한 설정이 없다면 'NEXT'
          ![3-17](/docs/WINDOWS/LAB_DHCP/3-17.png)  

          9. DHCP를 제공하는 클라이언트에게  DNS server IP나 Gateway IP를 제공 여부를 결정할수 있다. 제공을 원하면 'Yes'를 체크하고 다음 설정을 위해 'NEXT' 클릭.
          ![3-18](/docs/WINDOWS/LAB_DHCP/3-18.png)  

          10. DHCP를 제공받는 Clinet에게 함께 제공할 Gateway IP를 선택 할 수 있다. 입력란의 제공할 Gateway IP를 입력하고 'ADD'누른후 목록에 IP가 등록이 된것을 확인하자. 설정을 마치면 'NEXT'  
          ![3-19](/docs/WINDOWS/LAB_DHCP/3-19.png)

          11. Domain Name and DNS Servers에서는 DNS Server IP를 등록할수 있다. 그리고 Active Directory를 구성했을때 도메인도 등록할수 있다. 관련해서 Active Directory에서 다시 언급하겠다. 특별한 설정이 없다면 'NEXT'.  
          ![3-20](/docs/WINDOWS/LAB_DHCP/3-20.png)  

          12. WINS Server 설정 섹션이다. 특별사항이 없다면 'NEXT'  
          ![3-21](/docs/WINDOWS/LAB_DHCP/3-21.png)  

          13. 설정한 영역을 활성화 하고 싶은지 묻는 창이다. 'Yes'에 체크하고 'NEXT'누르자.
          ![3-22](/docs/WINDOWS/LAB_DHCP/3-22.png)  

          14. 설정이 성공적으로 됐다는 메세지를 확인하고 'Finish'를 클릭.  
          ![3-23](/docs/WINDOWS/LAB_DHCP/3-23.png)
  
5. 작동확인  
    * DHCP Server  
    \- Server Manager > DHCP 의 'Manageability'에 'Online - Performance counters not started'라도 되어 있다. 이뜻은 온라인에 연결을 되어 있으나. DHCP기능이 제대로 작동하고 있지 않다는 뜻이다. 제대로 작동 할수 있게 설정이 필요하다.
      1. Server Manager > DHCP 서버 목록에서 작동시킬 서버를 선택하고 우클릭  
      ![4-1](/docs/WINDOWS/LAB_DHCP/4-1.png)  

      2. 목록에서 'Start Performance Counters'를 찾아 클릭'  
      ![4-2](/docs/WINDOWS/LAB_DHCP/4-2.png)  

      3. 서버의 'manageability'의 부분이 'Online - Performanc counters not started' 가 'Online'으로 바꾸어지는것 확인.  
      ![4-3](/docs/WINDOWS/LAB_DHCP/4-3.png)  
    * Client Computers  
      1. 'Network Protocol Version 4 (TCP/IPv4) Properties'를 열어 'Obtain and IP address automatically'로 설정 되었는지 확인.  
      ![5-1](/docs/WINDOWS/LAB_DHCP/5-1.png)  

      2. [Windows key] + r을 눌러 'Run'을 실행하고, 명령어 입력 창에 'CMD'입력하고 엔터를 눌러 실행.  
      ![5-2](/docs/WINDOWS/LAB_DHCP/5-2.png)  

      3. Pop-up된 CMD창에 'ipconfig'입력후 실행시켜 네트워크 정보 출력. 하고 ping 192.168.102.10를 입력하여 DHCP Server간에 Ping 테스트.
      ![5-3](/docs/WINDOWS/LAB_DHCP/5-3.png)

      4. Clinet_2도 3.과 같이 테스트.
      ![5-4](/docs/WINDOWS/LAB_DHCP/5-4.png)

      5. DHCP Server로 돌아가서 Server manager > tool > DHCP > [computer name] > IPv4 > Scope[192.168.102.0]VLAN102 > Address Leases에서 DHCP로 IP를 공급받은 Client 리스트 확인 가능하다.
      ![5-5](/docs/WINDOWS/LAB_DHCP/5-5.png)
