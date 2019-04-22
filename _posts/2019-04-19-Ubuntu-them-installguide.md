---
layout: post
title:  "Ubuntu Costomizing Theme"
date: 2019-04-22
categories: Ubuntu
---
# **우분투 테마 꾸미기**

이번 포스팅은 우분투18.04 버전기준  lightDM display manager 대상으로 테마를 꾸미는 글입니다.  

먼저 우분투를 관리하는 tool을 설치하도록 합시다.  

`sudo apt install gnome-tweak-tool`  

`sudo apt install unity-tweak-tool`  

![](/img/gnome-tweak.png){: width="500"}  
**gnome tweak tool**

![](/img/unity-tweak.png){: width="500"}  
**unity tweak tool**

<br/>
사실 그놈 툴 기능을 유니티 툴에서 대부분 수행할 수 있어서 그놈 툴은 딱히 필요없긴하다..
그놈 툴은 그냥 시작 프로그램 쉽게 설치하는 용도 정도,,이긴한데 이것도 딱히 그놈툴을 사용할 필요는 없다.

![](/img/startup.png){: width="500"}  
*slack하나만 추가해뒀다.*  
~~사실 lightDM전에 gdm3을 사용해서 설치했었다가 지포스 관련 이슈로 ligthDM으로 넘어오면서 이거라도 써야지 하고 썼던게 더 큰것 같다,,,,~~

<br/>
이제 기본적인 준비는 끝났으니, 테마를 설치해보도록 합시다.

전 포스팅에서 잠깐 언급했던 paper와 Numix테마중 Numix테마 설치과정만 포스팅하고 paper는 설치 가이드 페이지만 링크하겠습니다.  
[Paper Theme 설치 가이드 페이지](https://itsfoss.com/install-paper-theme-linux/)


```
sudo add-apt-repository ppa:numix/ppa
sudo apt update
sudo apt install numix-gtk-theme numix-icon-theme-circle  
#아이콘 테마 설치원하시지 않는 분은 numix-gtk-theme만 입력해주세요. 아이콘도 예쁘니 설치 ㄱㄱ
```

터미널을 통해 설치를 완료했으면 유니티 툴을 실행시켜서 바꿔줍시다.

![](/img/numixtheme.png){: width="500"}
![](/img/numixicon.png){: width="500"}  
*Numix circle아이콘이 깔끔하고 좋아서 사용중입니다.*

![](/img/numixthemeset.png)
*Numix 아이콘과 테마를 설치한 화면*

<br/>
저는 여기서 더 깔끔하게 하고싶어서 **Plank**라는 맥북처럼 아래 독을 만들어주는 패키지를 설치했었는데  
결국 런쳐바를 완전히 없앨수는 없어서(숨기는것은 가능하지만 마우스가 근처갈시 자꾸 뜨는게 거슬림) 그냥 윈도우처럼 화면 하단에 런처바를 이동시켰습니다.

Plank 독 패키지 설치하고 싶으신 분은  
```
sudo add-apt-repository ppa:ricotz/docky
sudo apt update && sudo apt install plank
```
입력하시고 세팅해주시면 됩니다.  
세팅 방법은
`plank --preferences`를 터미널에 입력해주면 세팅 할 수 있습니다.

런쳐바는 유니티 툴에서 설정해 줄 수 있습니다.

![](/img/launcher.png)

<br/>

상단바도 Panel탭에 가면 수정가능합니다.  
저는 날짜표시쪽을 상세하게 하고 배터리부분도 좀 더 자세하게 보고싶어서 추가해줬습니다.

![](/img/panel.png)

<br/>
다음 우분투 포스팅은 터미널 커스터마이징 관련으로 올릴 예정입니다.
