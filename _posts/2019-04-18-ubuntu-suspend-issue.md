---
layout: post
title:  "Ubuntu 18.04  Suspend Issue"
date: 2019-04-18
categories: Ubuntu
---


# 우분투 18.04에서 발생하는 절전시 먹통 현상

<br/>
우분투는 현재 nVidia 그래픽 환경에서 많은 문제점을 포함하고있다.
<br/>
### 듀얼부팅으로 우분투 듀얼부팅시 freezing현상
먼저 첫번째로는 우분투를 듀얼부팅으로 설치할 때 발생한다.  
로딩화면에서 멈추거나 설치화면에 들어와서 멈추는 현상이 발생하게 되는데, 이 때 우분투 grub창이 열렸을때 e버튼을 눌러서 `quiet splash` 뒤에 `noveau.modeset=0` 을 입력하거나 `nomodeset acpi=off` 를 입력하고 f10을 누르면 정상적으로 진행이 된다.
<br/>
아마 16버전에서는 설치 후에도 grub 환경을 위와 동일하게 변경해주지 않으면, 시스템을 종료하거나, 설정파일을 열 때 freezing현상이 발생할 것이다.

<br/>
### gdm3환경에서 발생하는 suspend(화면 절전)시 발생하는 먹통 현상
18.04에서 display manager는 lightDM에서 gdm3 로 업데이트 되었다.
<br/>

![](/img/dismanager.png)

*리눅스 환경 가장 좋은 평을 받고있는 manager*

16.04에서 18.04로 넘어오면서  gdm3(GNOME Display Manager)의 직관적이고 깔끔한 display가 굉장히 마음에 들었다.

하지만 마음에 들어한것도 잠시,, display가 절전시 먹통이 되어 마우스포인터만 움직이는 현상이 발생되었다.

![](/img/suspend.jpg)

~~젠장~~

물론 종료도 안먹히고 전원버튼으로 강제종료를 해주어야한다.

이 문제로 구글링을 해본결과 수많은 유저들이 해당 이슈를 겪고 있고 다양한 해결방법들이 있었다.
오류원인이 너무 많기 때문에 하나하나 그 방법들을 해봐야했고,
<br/>
gdm3를 사용하려고 발악하다가 결국 모든 해결방법이 통하지 않아  
디스플레이 매니저를 lightDM으로 다시 바꿔야만했다,,,,
<br/>
이번  포스팅에서는 구글링을하면서 찾은 방법들에 대해 다루어보겠다.
<br/>

## 1. Nvidia Graphics Issue

이 현상은 Nvidia의 Nouveau 디스플레이 드라이버 때문에 발생하는 현상이다.
Nouveau 드라이버는 reverse-engineering을 통해 오픈 소스 프로젝트로 개발된 디스플레이 드라이버이다.  
하지만 현재 많은 리눅스 배포판이 Nouveau 드라이버가 GPU를 구동하는 경우에 에러가 발생하고있기 때문에 이 Nouveau 드라이버를 멈춰주는 것이 해결방법이다. 포럼에서는 Nvidia 드라이버가 최초설치되기 전에 Nouveau드라이버를 비활성화해야한다고 말하고있다.
<br/>
이 방법은 해외 포럼 글들을 살펴봤을때 가장 해결이 잘 된 방법 중 하나이다.
<br/>
**grub 수정**
- 터미널을 열고 아래 코드를 입력한다.  
`sudo nano etc/default/grub`
파일을 열고나서
`GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"` 이 부분을  
`GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nouveau.modeset=0"`
이렇게 수정하자.  
vi를 통해 수정하게되면 저장이 안되는 이슈가 발생한다고하니 일단 상단의 코드로 파일에 접근하자.
<br/>
수정을 완료한 후 Ctrl + o키를 누르고 Ctrl + x 키로 빠져나오자.  
그리고나서
`sudo update-grub`
를 입력해준뒤 우분투를 리부트한다.
<br/>
이 방법으로도 해결이 안된다면 
**/ect/modprobe.d** 폴더에 새파일을 만드는 방법이 있다.  
파일의 이름은 disable-nouveau.conf로 만들고, sudo를 통해 다음 코드를 작성하도록 하자.
```
blacklist nouveau
options nouveau modeset=0
```
그 후 
```
sudo update-initramfs -u
```
를 실행한 후 리부팅 해준다.
<br/>
만약 여기서 해결이된다면, 당신은 선택받은 사람 중 한명이 될 것이다.
<br/>
<br/>
## 2. s2idle Issue

이 현상은 컴퓨터가 절전모드에 들어갈 시 깊은 수면에 들어가지않고 s2idle 모드로 들어가는 문제이다.  
이는 간단하게 코드를 입력하면 확인할 수 있다.  

`cat/sys/power/mem_sleep`

이때 결과값이

`s2idle[deep]`으로 나온다면 이 부분에는 문제가 없다는 뜻이고, 대괄호 내부에 `s2idle`이 출력된다면 일시 중단되었다는 뜻이므로  
<https://askubuntu.com/questions/1029...036122#1036122>  
<br/>
해당 링크한 사이트에 들어가서 deep으로 수정해주도록 하자.  
<br/>
난 이 부분도 deep으로 되있어서 큰 이득을 얻지 못했다.
<br/>
<br/>
## 3. Kernel 버전을 바꾸어보기

이 방법으로 해결된 유저도 몇명있어서 소개해보곘다.  
이는 UKUU라는 프로그램을 통해 간단하게 Kernel 버전을 수정할수있고, 만일 오류가 발생했을 시 grub메뉴에서 기존 커널버전으로 다시 부팅할 수 있기때문에 커널바꿔서 우분투 접속이 안된다고 걱정할 필요는 없다.
<https://www.omgubuntu.co.uk/2017/02/ukuu-easy-way-to-install-mainline-kernel-ubuntu>해당 링크를 참고하여 설치한 후 구버전 커널을 설치해보도록 하자.  
많은 포럼에서 해결을 한 커널 버전은 4.14버전이라고하니 한번 설치하고 테스트해보자.

![](/img/UKUU.png)

<br/>
~~물론 나는 이 방법으로도 해결되지 않았다,,,ㅠㅠ~~
<br/>
<br/>

## 4. lightDM으로 돌아가기

이 방법은 내가 정말 하고싶지 않았던 방법이다.  
일단 lightDM은 slack새 알림이 뜰때 눌러도 크롬으로 연결되버리거나 반응하지 않기 떄문에, gdm3를 사용하다가 llightDM으로 다시 돌아오면 굉장히 불편하게 느껴진다.. 일단 기본 테마가 굉장히 별로다. 처음부터 gdm3를 경험하지 않았으면 좋았을텐데,,
```
sudo apt install ubuntu-unity-desktop
```
다음 코드를 입력하여 패키지를 설치해주고 display manager변경창이 뜨면 lightDM과 gdm3중에 선택하는 화면이 뜰것이다.  
선택지는없다. 여기까지 온 사람이면 미련 갖지말고 ligthDM으로 돌아가자.
이후 재부팅하면 16.04에서 지겹게 봐왔던 lightDM잠금화면이 왜 이제왔냐면서 우리를 반겨줄 것이다.  
^0^/
<br/>
unity-tweak-tool패키지를 설치하면 왼쪽에 자기자리 뽐내고있는 런처도 숨길수 있고 lightDM도 예쁘게 꾸밀수 있다.  
개인적으로 lightDM은 **paper테마**와 **Numix테마와 아이콘**이 깔끔하고 좋다.  
테마 설치는 다음 포스팅에서 다루기로,,  
<br/>
혹시나 gdm3로 돌아가고 싶으면 다음 코드들을 차례대로 입력하자.  
```
sudo apt purge ubuntu-unity-desktop
sudo dpkg-reconfigure gdm3 #gdm3선택하는 화면이 뜬다.
sudo apt purge lightdm
sudo apt autoremove
```
<br/>
아직까지 해외 포럼에는 이 이슈 해결을 바라는 글들이 올라오긴 하지만,,,  
언제 해결될지 모르니 그냥 속 편하게 lightDM으로 피난을 가자.
