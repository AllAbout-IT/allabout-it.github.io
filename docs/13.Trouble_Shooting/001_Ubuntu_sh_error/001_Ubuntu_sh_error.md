---
layout: default
title:  Ubuntu bash operating error
parent: Trouble_Shooting
-
# grandparent: VMware

# has_children: true

nav_order: 101

# permalink: /docs/PROJECT

---

# Ubuntu bash operating error

{:no_toc }

<details open markdown="block">  
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC  
{:toc}
</details>

이 에러는 Linux에서 bash스크립트를 만들고 sh 명령어로 실행했을때 나타나는 error이다.
증상은 bash 스크립트 작성시에 사용되는 기호(예: (), {}등)이 에러의 원인이 되나. chmod +x로 시스템이 파일을 실행할 권리를 주고 파일을 호출할때에는 실행이 됩니다.

```sh
#!/bin/bash

function print() {

  echo $1

}

print "I can speak English

```

Error Message
![1](/docs/13.Trouble_Shooting/001_Ubuntu_sh_error/pic/1.png)

이와 같은 증상은 'sh' 명령어 사용시 Bash가 아닌 다른 쉘에 지정이 되어 있을 가능성이 있다.

그렇다면, 이와 같은 명령어로 시도해 볼수 있다.

```sh
sudo dpkg-reconfigure dash
```

![2](/docs/13.Trouble_Shooting/001_Ubuntu_sh_error/pic/2.png)

The system shell is the default command interpreter for shell scripts.

시스템 셸은 셸 스크립트의 기본 명령 인터프리터입니다.

Using 'dash' as the system shell will improve the system's overall performance. It does not alter the shell presented to interactive users.

'dash'를 시스템 셸로 사용하면 시스템의 전반적인 성능이 향상됩니다. 대화형 사용자에게 제공되는 셸을 변경하지 않습니다.

Use dash as the default system shell?

'대시'를 기본 시스템 셸로 사용하시겠습니까?

위 와 같은 메세지를 통해서 Ubuntu에서는 시스템 쉘이 'dash'로 사용되고 있다는 것을 알수 있다. 

여기에서 'No'를 선택한다.

그리고 난 뒤 sh [filename.sh]를 실행하면
![3](/docs/13.Trouble_Shooting/001_Ubuntu_sh_error/pic/3.png)

sh 명령어로 bash 함수가 정의되어 있는 .sh 스크립트가 정상으로 작동이 되어지는 것을 확인 할수 있다.