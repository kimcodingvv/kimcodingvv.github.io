---
layout: post
title : "내가 보려고 쓰는 우분투 초기설정"
excerpt : "에러 그만..."
date : 2020-03-22-01:48
tags : [Ubuntu Setting]
category : [Ubuntu]
comments : true
author: Kimcoding
feature: /assets/img/post/ubuntu.webp
no-repeat : true
catalog : true
---



## 서론

<br/>

최근에 업데이트를 하면서 오류가 나서 이것저것 만지다가 결국 재설치를 하게 되었는데 그 후로 이것저것 해보면서 재설치를 자주하고 있네요...

<br/>

사용하다가 빼먹은걸 찾기도 하고...

그때마다 기억을 더듬어가며 초기설정을 하며 다운받고 설정하고 하는게 불편해서 그냥 글을 써놓으려고 합니다.

---

<br/>

## 1. NVIDIA 그래픽 드라이버

<br/>



![](https://user-images.githubusercontent.com/57852139/77232646-a8173f00-6be5-11ea-8964-fbdaa4c03367.png)

<br/>

nvidia 드라이버 설치를 `gnome tweak tool`에서 설정해도 된다고 들었지만 터미널로 급하게 할 때가 있기 때문에...

<br/>

```shell
$ ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0 ==
modalias : pci:v000010DEd00001C8Dsv00001043sd000013B1bc03sc00i00
vendor   : NVIDIA Corporation
model    : GP107M [GeForce GTX 1050 Mobile]
driver   : nvidia-driver-440 - third-party free recommended
driver   : nvidia-driver-390 - third-party free
driver   : nvidia-driver-415 - third-party free
driver   : nvidia-driver-410 - third-party free
driver   : nvidia-driver-435 - distro non-free
driver   : xserver-xorg-video-nouveau - distro free builtin
```

<br/>

추천 드라이버가 `nvidia-driver-440`이라고 합니다. 5시간 전에는 435라고 했는데...?

<br/>

```shell
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt update
$ apt-cache search nvidia | grep nvidia-driver-440 // 설치 가능한 드라이버인가?
$ sudo apt-get install nvidia-driver-440
$ sudo reboot
```



---

<br/>

## 2. 크롬 설치

<br/>

**[크롬 공식 사이트](https://www.google.com/intl/ko/chrome/)**

<br/>

웹 브라우저는 크롬!

크롬 공식사이트에서 deb파일을 받아서 다운로드하시면 됩니다.

<br/>

터미널 다운 방법은 [https://webnautes.tistory.com/1184](https://webnautes.tistory.com/1184) 참고하세요! 깔끔!



---



<br/>

## 3. 한영 키보드

<br/>



`UIM`을 사용하고 있고 자세한 내용은 따로 올리겠습니다.

<br/>

**[우분투 한글, 한영키](https://kimcodingvv.github.io/Ubuntu-UIM)**



---



<br/>



## 4. Gnome Tweak Tool

<br/>



```shell
$ sudo apt install gnome-tweak-tool
```



---

<br/>

## 5. Terminator

<br/>

```shell
$ sudo apt install terminator
```

<br/>

**터미네이터 사용자 설정**

```shell
$ gedit ~/.config/terminator/config
```

<br/>

대충 이 정도...? 했습니다

```
[global_config]
  dbus = False
  sticky = True
  tab_position = bottom
[keybindings]
[layouts]
  [[default]]
    [[[child1]]]
      parent = window0
      profile = default
      type = Terminal
    [[[window0]]]
      parent = ""
      type = Window
[plugins]
[profiles]
  [[default]]
    background_darkness = 0.75
    background_type = transparent
    cursor_color = "#aaaaaa"
    scroll_on_output = True
    scrollbar_position = hidden
```





---



<br/>

## 6. D2Coding

<br/>

**[D2Coding Git](https://github.com/naver/d2codingfont)**



글꼴 다운로드 후 ttf파일로 설치



---

<br/>

## 7. 마우스 휠 속도

<br/>

```shell
$ sudo apt-get install imwheel
$ gedit ~/.imwheelrc // 스크롤 속도 설정
```

<br/>

**스크롤 속도를 설정**합니다. 좀 답답해서 저는 4로 설정했는데 충분한 듯 합니다.

```
".*"
None,      Up,   Button4, 4
None,      Down, Button5, 4
```

<br/>

**부팅 시에 imwheel 자동 실행**

```shell
$ sudo gedit /etc/X11/imwheel/startup.conf
```

파일에서

```
IMWHEEL_START=0 -> IMWHEEL_START=1
```

<br/>

**수정한 내용 적용**

```shell
$ imwheel -k
```



---



<br/>

## 8. VIM



```shell
$ sudo apt-get install vim
```



---

<br/>

## 9. Gnome Shell Extension

<br/>

```shell
$ sudo apt install chrome-gnome-shell
```

<br/>

[Chrome 그놈 쉘 확장](https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep?hl=ko)

<br/>

추가를 하고 아이콘 클릭하면 사이트로 갑니다.

<br/>

[https://extensions.gnome.org/](https://extensions.gnome.org/)

<br/>

제가 설치한 목록

+ [AlternateTab](https://extensions.gnome.org/extension/15/alternatetab/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Alt + Tab 했을 때 화면도 보여줍니다
+ [Caffeine](https://extensions.gnome.org/extension/517/caffeine/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;화면보호기 비활성화
+ [Clipboard Indicator](https://extensions.gnome.org/extension/779/clipboard-indicator/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;클립보드 리스트와 검색
+ [Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;독(Dock)을 다양하게 설정
+ [Drop Down Terminal](https://extensions.gnome.org/extension/442/drop-down-terminal/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;상단에서 터미널 창
+ [Dynamic Top Bar](https://extensions.gnome.org/extension/885/dynamic-top-bar/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;상단 바 투명도 설정
+ [Extensions](https://extensions.gnome.org/extension/1036/extensions/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;상단 바에 확장 프로그램 설정
+ [GSConnect](https://extensions.gnome.org/extension/1319/gsconnect/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;갤럭시와 연결 (아이폰은 안되는 듯 합니다..)
+ [OpenWeather](https://extensions.gnome.org/extension/750/openweather/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;상단 바에 날씨
+ [Refresh Wifi Connections](https://extensions.gnome.org/extension/905/refresh-wifi-connections/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;연결 가능한 와이파이 리스트 새로고침
+ [Screenshot Tool](https://extensions.gnome.org/extension/1112/screenshot-tool/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;스크린샷
+ [Sound Input & Output Device Chooser](https://extensions.gnome.org/extension/906/sound-output-device-chooser/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;입출력 장치 설정
+ [Ubuntu AppIndicators](https://extensions.gnome.org/extension/1301/ubuntu-appindicators/)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;이건 뭐지...

<br/>

굉장히 설치를 많이 했었네요...



---



<br/>

## 10. Intellij, Clion, Typora

<br/>

우분투 소프트웨어 센터에서 설치하시면 됩니다. 갓갓



---

<br/>

## 11. 테마 설정

<br/>



**[우분투 꾸미기](https://kimcodingvv.github.io/Ubuntu-Theme/)**



---

<br/>

이 정도가 있을까요..?

몇 개 까먹었을 수도 있지만 그런 경우 추후에 수정해야겠네요

<br/>

참고하실분들은 참고하세요!