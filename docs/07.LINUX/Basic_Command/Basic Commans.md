---
layout: default
title: 01_Basic Commands 
# nav_order: 2
parent: LINUX
---
<h1>01 Ubuntu Basic Commands</h1>  

<br>

1. 도움말 보기 (man)  
```$ man <검색할 명령어>```  
\- man은 manual의 약어.    

    ```$ man mv```  
    \- 명령어 'mv'의 manual  
    <br>  
    ![man01](/docs/LINUX/Basic_Command/man01.png)  
    \- 명령어 'mv'에 대한 모든 내용을 출력.  
<br>
<br>
<br>
2. 파일 목록 보기 (ls)  
```$ ls <옵션><파일|디렉토리>```  
<br>
    2.1 -a  
    * 숨김파일까지 출력  
    ```$ ls -a```
    <br>    
    ![la-a](/docs/LINUX/Basic_Command/la-a.png)  
    \- ' . (dot)'으로 시작하는 파일명은 숨김파일의 이름이다.    

    2.2 -l  
    * 파일/디렉토리의 자세한 정보 출력(type, permission, link, size, owner)   
    ```$ ls -l ```
    <br>  
    ![ls-l](/docs/LINUX/Basic_Command/ls-l.png)  
      
    2.3 -l \<Path>
      * Path 안에 있는 파일 리스트의 자세한 정보 출력.  
      ```$ la -l /1```
      <br>  
      ![ls -l path](/docs/LINUX/Basic_Command/ls-lpath.png)  

    2.4 -R  
    * 하위 디렉토리까지 모두 출력
    ```$  ls -R```
    <br>  
    ![ls-R](/docs/LINUX/Basic_Command/ls-R.png)  
<br>
<br>
<br>

3. 디렉토리 생성 (mkdir)  
```$ mkdir <option> <path>```  
<br>
    3.1. \<name>(직속 하위 폴더)  
    - 기본 디렉토리를 생성    
    ```$ mkdir 1/tmp```  
    ![mkdir<path>](/docs/LINUX/Basic_Command/mkdir<path>.png)  
    \- 디렉토리를 생성할 부모 폴더는 반드시 만들기 전에 있어야 한다.  

    3.2 -p  
    - 존재하지 않는 부모 디렉토리도 함께 생성  
    ```$ mkdir -p 1/guru/bin```  
    ![mkdir-R](/docs/LINUX/Basic_Command/mkdir-p.png)  
    \- bin의 상위폴더 /guru가 없어도 한번에 생성된것을 확인.  

    3.3 -m 
    * 디렉토리 생성시 권한부여 가능  
    ```$ mkdir -m 777 1/share```  
    ![mkdir-m](/docs/LINUX/Basic_Command/mkdir-m.png)  
    \- 앞서 생성된 다른 폴더들과 다른 권한을 가진 폴더가 생성되었다.  
<br>
<br>
<br>
4. 빈 디렉토리 삭제  
```$ mkdir <option> <path>```  
<br>
    4.1 \<name>(직속 하위 폴더)  
    * 기본 빈 디렉토리 삭제  
    ```$ rmdir 1/share/```  
    ![rmdir](/docs/LINUX/Basic_Command/rmdir.png)  
    \- guru와 tmp 사이에 있던 share폴더가 삭제 되었다.  
    \- rmdir은 삭제대상의 폴더가 반드시 비워져 있어야 실행한다.  

    4.2 -p   
    * 비어있는 부모 디렉토리도 함께 삭제  
    ```$ rmdir -p 1/guru/bin```
    ![rmdir-p](/docs/LINUX/Basic_Command/rmdir-p.png)  
    \- rmdir: failed to remove directory '1': directory not empty  
    \- 디렉토리 '1'비워 지지 않아서 삭제에 실패 했다고 한다.  
    \- 하지만, 검색을 해보면 비워져 있는 /guru/bin 경로가 모두 지워져 있는 것을 확인 할수 있다.  
<br>
<br>
<br>

5. 디렉토리 이동  
```$ cd <path>```  
<br>
    5.1. $HOME
    * 사용자의 HOME 디렉토리로 이동  
    ```$ cd $HOME```  
    ![cd$HOME](/docs/LINUX/Basic_Command/cd$HOME.png)  
    \- 떨어진 곳에 있어도 cd $HOME을 이용해서 한번에 홈폴더로 이동할수 있다.  
    \- 'pwd'는 현재 자신의 path 위치를 알려주는 명령어이다.

    5.2. -
    * 이전 작업 디렉토리로 이동  
    ```$ cd - ```
    <br>  
    ![cd-](/docs/LINUX/Basic_Command/cd-.png)  
    \- 거리에 상관 없이 한번에 위치가 움직인다.  
      
    5.3. ..
    * 상위 디렉토리로 이동  
    ```$ cd ..```
    <br>  
    ![cd..](/docs/LINUX/Basic_Command/cd...png)
<br>
<br>
<br>
6. 파일복사하기 (cp)  
``` $ cp <option> <원본파일이름> <목적지파일이름>```
<br>  
    6.1. cp \<path/name> <path/name>
    * 기본 파일 복사  
    ``` $ cp findtest/2/tmp/usr/sample test/1/sample```
    <br>  
    ![cp](/docs/LINUX/Basic_Command/cp.png)  

    6.2. -i  
    * 복사할때 overwrite 할 것인지 질문  
    ```$ cp -i test/1/sample test/2/tmp/usr/sample```
    <br>  
    ![cp-i](/docs/LINUX/Basic_Command/cp-i.png)
    \- 6.1 번에서 복사를 받았던 곳에 다시 복사를 하였다.

    6.3. -f  
    * 복사할때 overwrite 질문 없이 무조건 덮어쓰기
    ```cp -f test/1/sample test/2/tmp/usr/sample```
    ![cp-f](/docs/LINUX/Basic_Command/cp-f.png)
<br>
<br>
<br>
7. 파일 이동하기 & 파일 이름변경 (mv)  
``` $ mv <option> <target path/name> <new filename>```
<br>  
    7.1. \<target path/name> \<new path/new filename>
    * 기본 이동
    ``` $ mv mv test/1/bin/ test/2/bin ```
    ![mv](/docs/LINUX/Basic_Command/mv.png)
    * 물론 폴더 뿐만 아니라 파일도 가능  
    ``` $ mv $ mv test/1/sample test/2/bin/sample```  
    ![mv2](/docs/LINUX/Basic_Command/mv2.png)

    7.2. -i 
    * 이름을 바꿀때 overwrite 할 것인지 질문  
    ``` $ mv -i test/2/bin/sample test/1/table ```
    ![mv-i](/docs/LINUX/Basic_Command/mv-i.png)
<br>
<br>
<br>
8. 파일 & 디렉토리 삭제하기 (rm)  
```$ rm <option> <path/filename>```
<br>  
    8.1  $ rm \<path/filename>
    * 지정된 파일 또는 디렉토리가 삭제
    ![rmfile](/docs/LINUX/Basic_Command/rmfile.png)  
    \- 커맨드 이후 타킷이된 파일이 제자리에 없어진 것을 확인.  

    8.2 -f  
    * 하위 내용을 포함한 디렉토리 삭제  
    ``` $ rm -r test/2/bin/```
    ![rm-f](/docs/LINUX/Basic_Command/rm-f.png)
<br>
<br>
<br>
9. 파일찾기 (find)  
```$ find <경로> <옵션> <조건> <실행종류>```
<br>  
    9.1 -name  
    * 현재 디렉토리에서 'big'가 포함되는 파일 찾기  
      ```$ find -name "*big*"```
    ![find-name](/docs/LINUX/Basic_Command/find-name.png)  
    * 현재 디렉토리에서 .txt가 확장자 모두 찾기  
      ```$ find . -name "*.txt"```
      ![find](/docs/LINUX/Basic_Command/find-name-0.png) 
      
    9.2 -type *.\<format type>  
      \- 타입별로 검색.  
     * 현재 디렉토리에서 모든 디렉토리 찾기  
      ```$ find . -type d```   
      ![type_01](/docs/LINUX/Basic_Command/find-type_01.png)  

    * 현재 디렉토리에서 모든 파일 찾기  
      ```$ find . -type f```  
      ![type_02](/docs/LINUX/Basic_Command/find-type_02.png)  
      \> 하위 폴더 내의 파일 리스트도 출력
      \> 폴더는 검색되지 않음

    9.3 -size  
      \- 특정 크기의 파일을 검색.

      * 현재 디렉토리에서 1024byte인 파일 검색  
      ```$ find . -size 1024c```  
      ![size_01](/docs/LINUX/Basic_Command/find-size_01.png)  
      
      * 현재 디렉토리에서 +1024c보다 큰 파일 검색  
      ```$ find . size +1024c ```  
      ![size_02](/docs/LINUX/Basic_Command/find-size_02.png)  

      * 현재 디렉토리에서 1024byte보다 작은 파일 검색  
      ```$ find . size -1024c```
      ![size_03](/docs/LINUX/Basic_Command/find-size_03.png)