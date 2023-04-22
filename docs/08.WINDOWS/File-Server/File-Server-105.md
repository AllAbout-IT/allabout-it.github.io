---
layout: default
title: File Server in WINDOWS
nav_order: 105
parent: WINDOWS
---
# File Server in Windows  
{: .no_toc }  
<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>  

## Introduction  
###

## Building NFS File Server in Windows Server 2016  

### Preparation for work  

  1. File Server  
  \- Adding 100G physical storage  
  \- OS : Windows Server 2016  
  \- IP : 192.168.111.10  
  \- Turn off all firewall in OS

  2. Client Server  
  \- OS : Windows Enterprise 10  
  \- IP : 192.168.111.20  
  \- Turn off all firewall in OS

### Adding physical hard storage in VMware fusion  

  1. The machine has to turn off before beginning.

  2. NFS Server > Settings > Added Device  
  ![1](/docs/WINDOWS/File-Server/1.png)  

  3. Select 'New Hard Disk' in Settings > Added Device and then, click 'Add'.
  ![2](/docs/WINDOWS/File-Server/2.png)  

  4. Put '100' into blank box for disk size. and then, click 'Apply'.  
  ![3](/docs/WINDOWS/File-Server/3.png)

  5. Close window

### Registration added hard storage to Windows Server  

  1. Turn on The Server machine(Windows Server 2016) in WMware.  

  2. Press 'Window key' and put 'Disk management' or 'create and format' and then, press 'Enter key' or click the icon on the list for running application.
  ![6](/docs/WINDOWS/File-Server/6.png)

  3. Select 'GPT(GUID Partition Table)' and click 'OK' in 'Initialize Disk' pop-up window.
  ![7](/docs/WINDOWS/File-Server/7.png)  

  4. Check the new disk drive that was added from Vmware and right-click on the new disk drive section then, click 'New Simple Volome'.  
  ![8](/docs/WINDOWS/File-Server/8.png)  

  5. Click 'Next' on the New Simple Volume Wizard pop-up window.  
  ![9](/docs/WINDOWS/File-Server/9.png)  

  6. Put disk size you want into blank box on 'Specify Volume Size' section and then click 'Next'  
  ![10](/docs/WINDOWS/File-Server/10.png)

  7. In the 'Assign Drive Letter or Path' section, select 'Assign the following drive letter' and then choose the letter for the new drive volume. You can also choose other options, such as making the volume a folder under an existing volume, or a volume without a name. click 'Next' after done selection.
  ![11](/docs/WINDOWS/File-Server/11.png)  

  8. In the 'Format Partition', select 'Format this volume with the following settings'. and put a new 'Volume label' name(ex>NFS-Server-Test), and let the rest of them as the default setting. then, click 'Next'.  
  ![12](/docs/WINDOWS/File-Server/12.png)  
  [If you want to know more about 'Format'. Click here](/)  

  9. Check the all configurations you did in this window. and then, click 'Finish'.  
  ![13](/docs/WINDOWS/File-Server/13.png)  

  10. Close 'Disk Management' window.

### Installation NFS Server in Server Manager  

  1. press 'Window key' on the keyboard and put 'Server manager' then click 'Server Manager' on the list for running.
  ![16](/docs/WINDOWS/File-Server/16.png)  

  2. At the Server Manager window click on 'Manage'. then, click 'Add Roles and Features'.
  ![11](/docs/WINDOWS/File-Server/17.png)  

  3. At the 'Add Roles and Features Wizard'on the pop-up window, check the things you need to do before proceeding in the 'Before you begin' section, then click 'Next'.
  ![12](/docs/WINDOWS/File-Server/18.png)  

  4. Select 'Role-vased or feature-based installation'. and click 'Next'.  
  ![18-1](/docs/WINDOWS/File-Server/18-1.png)
  
  5. At 'Select destination server' Section, Select 'Select a server from the server pool'. and select the server you want to install roles and features after checking the information (Name, IP Address, Operating System) on the 'Server Pool' list. and then, click 'Next'.  
  ![19](/docs/WINDOWS/File-Server/19.png)  

  6. At 'Remove server roles', select 'Server for NFS in 'File and Storage Services > File and iSCSI Services' on the Roles list. and then, click blank check box on the left.
  ![20](/docs/WINDOWS/File-Server/20.png)  

  7. Click 'Next' after checking the installation information on the new pop-up window.  
  ![21](/docs/WINDOWS/File-Server/21.png)  

  8. Click 'Next' on the returned window.
  ![22](/docs/WINDOWS/File-Server/22.png)  

  9. Click 'Next' at 'Select features'
  \- You don't need any selection here due to you already installed the feature you want in the before step.  
  ![23](/docs/WINDOWS/File-Server/23.png)  

  10. Click 'Install' at 'confirm installation selections'  
  ![24](/docs/WINDOWS/File-Server/24.png)  

  11. Wait for a while for feature installation and click 'Close' after succeed it.
  ![25](/docs/WINDOWS/File-Server/25.png)  

  12. Click 'File and Storage Service' on sidebar in Server Manager.  
  ![52](/docs/WINDOWS/File-Server/52.png)  

  13. You can see the server status on the list. right-click on the server selected. and then, find and click 'Start Performance counter' for running.
  ![53](/docs/WINDOWS/File-Server/53.png)  
  
  14. Ckeck the server status changed to 'online'.  
  ![54](/docs/WINDOWS/File-Server/54.png)  

### Configration Server for NFS in Windows Server

  1. Press 'Window Key' and put 'server manager' into blank search box. and then, press 'Enter key' or Click 'Server manager' icon on the list for running 'Server Manager'  
  ![35](/docs/WINDOWS/File-Server/35.png)

  2. Click 'File and Storage Services' on the sidebar.
  ![36](/docs/WINDOWS/File-Server/36.png)  

  3. Select 'To create a file share, start the New Share Wizard' after clicking 'Shares' on the second sidebar.
  ![37](/docs/WINDOWS/File-Server/37.png)  

  4. Select 'NFS Share - Quick' on the 'File share profile' list at the 'Select the profile for this share' Section in the 'New Share Wizard' pop-up window. and click 'Next' after done.  
  {: .flex-justify-around }
  ![38](/docs/WINDOWS/File-Server/38.png)  

  5. Check the Server that you want to share and select 'Share location' and then, choose The drive you want to share through the NFS Server. Also, you can make a 'custom path' through one other option.  
  ![39](/docs/WINDOWS/File-Server/39.png)

  6. Put 'Shared Name' you want(ex> NFS-Text) into blank on the box on the most top.  
  ![40](/docs/WINDOWS/File-Server/40.png)

  7. Check box 'No server authentication(AUTH_SYS)', 'Enable unmapped user access' and select 'Allow unmapped user access by UID/GID' at 'Specify authentication methods' section. and click 'Next' after done.  
  ![41](/docs/WINDOWS/File-Server/41.png)  

  8. Click 'Add' Specify the share permissions' section. and it'll open the 'Add Permissions new pop-up window. and then, put the client computer's IP address that you want to connect with the file server into the blank box under 'Host'. and next, select 'Read/Write' under 'Share permissions' through a click. click 'Add' after done.
  ![42](/docs/WINDOWS/File-Server/42.png)  

  9. Check the information that was configured on the list. and then, click 'Next.
  ![43](/docs/WINDOWS/File-Server/43.png)

  10. Check the information about permissions at the 'Specify permissions to control access' and then click 'Next' after done.  
  ![44](/docs/WINDOWS/File-Server/44.png)

  11. Check the configure information about Server, Client on the window at the 'Confirm selection' section. and then, click 'Create' after done.
  ![45](/docs/WINDOWS/File-Server/45.png)

  12. Check the task monitoring information on the list and then, click 'Close' after done.  
  ![46](/docs/WINDOWS/File-Server/46.png)  

  13. Check the task information that was configurated on the 'Shares'list.
  ![47](/docs/WINDOWS/File-Server/47.png)  

### Installation NFS Client on Client Computer  

  1. Turn on the client machine(Windows 10 Enterprise) in WMware.  

  2. Press [Window Key] + R for running 'Run' dialog type application.
  ![26](/docs/WINDOWS/File-Server/26.png)

  3. Put 'cmd' into the blank box and press the 'Enter key' or click 'OK' to run the 'CMD' application.
  ![27](/docs/WINDOWS/File-Server/27.png)  

  4. Put 'ipconfig' into the prompt and 'Enter key' to show IP configured. and check IP address.  
  ![28](/docs/WINDOWS/File-Server/28.png)

  5. put 'ping 192.168.111.10' and 'Enter key' for ping test with 'NFS Server'  
  ![29](/docs/WINDOWS/File-Server/29.png)  
  \-  If you did not succeed in the ping test with the right IP configuration. probably, It caused a firewall. check the firewall status again. or If you want work to include running a firewall, click this. [this](/)

  6. close 'CMD' Application

  7. Press [Window Key] and put 'features on'. If you can see 'Turn windows features on or off' click it on the list.
  ![30](/docs/WINDOWS/File-Server/30.png)

  8. Select 'Client for NFS' under 'Service for NFS' on the list at the 'Windows Features' pop-up window. and click 'OK'.  
  ![31](/docs/WINDOWS/File-Server/31.png)

  9. wait for a while until appying is done. and then, click 'Close'
  ![32](/docs/WINDOWS/File-Server/32.png)

### Setting up Client for NFS in Client Computer

  1. Press 'Window key' + E for openning 'File explorer'  
  ![33](/docs/WINDOWS/File-Server/33.png)  

  2. Find and click 'This PC' on the sidebar. select the 'Computer' tab at the top of the window and click the 'Map network Drive' icon on the function list.
  ![34](/docs/WINDOWS/File-Server/34.png)  

  3. Choose the letter of the drive, and put '\\[server ip]\[share name]' into the blank box next to 'Folder'. and click 'finish' after done.
  ![51-1](/docs/WINDOWS/File-Server/51-1.png)  
  \- It is configuration without security. you can make more secure configuration through 'Active Directory'.  

  4. If it succeeded in connecting. you can see like below status in 'File explorer'.  
  ![55](/docs/WINDOWS/File-Server/55.png)

### Testing

  * Make any file in NFS Drive on Client's computer. and then, if it succeeded it. you can check the status like this on Client computer and Server.  
  ![56](/docs/WINDOWS/File-Server/56.png)

## Building iSCSI File Server in Windows Server 2016  

### Testing