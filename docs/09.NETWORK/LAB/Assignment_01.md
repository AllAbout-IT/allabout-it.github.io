---
layout: default
title: Assignment_01
nav_order: 1
parent: LAB
grand_parent: NETWORK
---

LAB-01
======
Router
------

### 문제1. PC1, PC2간에 통신 되도록 구성합니다. 

1. 기본구성사항  
    - Router1대, Switch 1대, PC2대  
    - PC1. 1.1.1.1 255.255.255.0  
    - PC2. 1.1.1.2 255.255.255.0

2. 이블 연결 사항
    - PC1 FastEthernet0 ---(Copper Straight-Through)--- Switch FastEthernet 0/1  
    - PC2 FastEthernet0 ---(Copper Straight-Through)--- Switch FastEthernet 0/2  
    - Switch FastEthernet 0/3 ---(Copper Straight-Through)--- Router FastEthernet 0/0   

3. STEP.1  PC 설정  
\- IP, Subnet mask, Gateway를 설정합니다.  

    - PC1  
          1. PC1를 좌더블클릭 후 설정창을 연다.  
          2. 상단 메뉴에서 'Desktop'선택.  
          3. 목록에서 'IP Configuration'선택  
          4. 'IPv4 Address' 입력창에 '1.1.1.1'을 입력  
          5. 'Subnet Mask' 입력창에 '255.255.255.0'을 입력  
          6.  왼쪽 상단의 'X'를 눌러 창을 닫는다.  

    - PC2  
          1.  PC2를 좌더블클릭후 설정창을 연다.  
          2.  상단 메뉴에서 'Desktop'선택.  
          3.  목록에서 'IP Configuration'선택  
          4.  'IPv4 Address' 입력창에 '1.1.1.2'을 입력  
          5.  'Subnet Mask' 입력창에 '255.255.255.0'을 입력  
          6.  왼쪽 상단의 'X'를 눌러 창을 닫는다.  

    - CHECK!!  
    \- CMD창에서 ipconfig로 설정을 확인합니다.

4. STEP2. SWITCH 설정  
\-  현재 구성도에서 SWITCH는 설정이 필요 없습니다.  

5.STEP3. Router 설정  
Fa0/0 1.1.1.254를 설정합니다.  
Fa0/1 1.1.2.254를 설정합니다.