---
layout: post
title : "우분투 꾸미기 (테마 설정, Plank)"
excerpt : "이쁘다"
date : 2020-03-22-05:00
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



`Dash to Dock`을 사용하여 Dock을 쓰고 있었는데 어쩌다가 `Plank`를 알게 되었습니다.

그래서 구글링을 하여 [감성 프로그래밍 - Plank](https://programmingsummaries.tistory.com/359),  [감성 프로그래밍 - 테마 설정](https://programmingsummaries.tistory.com/360) 을 참고하여 `Plank`를 적용하다가 테마도 이뻐서 적용하게 되었습니다.

<br/>

블로그도 이뻐요... 갓갓...

<br/>

자세한 설명과 적용 방법, 테마 추천은 위에 링크한 감성 프로그래밍님 블로그에 있습니다!

저는 참고하여 대충 적용만...  한 번 끄적여보겠습니다!



---

<br/>



## Plank

<br/>

설치를 먼저 해보겠습니다.

```shell
$ sudo add-apt-repository ppa:ricotz/docky
$ sudo apt-get update
$ sudo apt-get install plank
```

<br/>

설치가 완료되었으면 설정을 해줍니다.



```shell
$ plank --preferences
```

<br/>

![](https://user-images.githubusercontent.com/57852139/77236080-7363b180-6bfe-11ea-96f1-796b539696c3.png)

<br/>

전 이렇게 설정했습니다.

<br/>

설정까지 완료하셨으면 원하는대로 모양이 나왔을텐데 원래있던 독이랑 겹칠수도 있습니다.

그래서 저는 `Dash to dock`을 설정하여 원래있던 독을 안보이게 했습니다.

<br/>

![](https://user-images.githubusercontent.com/57852139/77236132-0866aa80-6bff-11ea-82bf-f37473736f55.png)

<br/>

![](https://user-images.githubusercontent.com/57852139/77236145-2f24e100-6bff-11ea-963f-0e15c135d95c.png)

<br/>



이렇게 설정하시면 독이 보이지 않습니다.

<br/>

`Plank`를 실행해야 보일 겁니다.

그래서 시작 프로그램으로 설정하여 부팅 시에 자동 실행하도록 했는데 안될 때도 있어서 될 때까지 부팅하다보니 더 귀찮아지는 것 같아 부팅하고 `ALT + F2`에서 `plank` 명령어를 실행해서 사용하고 있습니다.

<br/>

하지만 저만 시작 프로그램에서 안되는 것일수도 있으니...

<br/>

![](https://user-images.githubusercontent.com/57852139/77236208-e4f02f80-6bff-11ea-8e98-29ceae61e17e.png)

<br/>

추가하게 되면 따로 설정하지 않아도 바로 Plank Dock이 보입니다.

---



<br/>



## 테마 설정

<br/>

**아이콘 설정**

<br/>

**[Numix Circle Git](https://github.com/numixproject/numix-icon-theme-circle)**

```shell
$ sudo add-apt-repository ppa:numix/ppa
$ sudo apt update
$ sudo apt install numix-icon-theme-circle
```

<br/>

설치가 완료되면 gnome-tweak-tool (기능 개선)에서 설정하시면 됩니다.

<br/>

![](https://user-images.githubusercontent.com/57852139/77236361-2d5c1d00-6c01-11ea-96ee-9ebb4658a106.png)

<br/>

탭에 설치한 아이콘 테마가 없다면 재부팅하시면 보입니다.



<br/>



**프로그램 테마**

<br/>

**[Arc Theme](https://github.com/horst3180/Arc-theme)**

<br/>

설치하기 전에 `autoconf`  `automake`  `pkg-config` `libgtk-3-dev` `git` 을 설치해줍니다.

<br/>

그 후에 테마를 설치하시면 됩니다.



```shell
$ git clone https://github.com/horst3180/arc-theme --depth 1 && cd arc-theme
$ ./autogen.sh --prefix=/usr
$ sudo make install
```

<br/>

![](https://user-images.githubusercontent.com/57852139/77236445-f3d7e180-6c01-11ea-9de3-e65548429058.png)



<br/>이것도 안보이신다면 재부팅하시면 됩니다!



---



<br/>

![](https://user-images.githubusercontent.com/57852139/77236464-136f0a00-6c02-11ea-848e-64a982185c94.png)

<br/>

저도 알록달록한걸 좋아해서 배경을 알록달록하게 바꿔봤습니다 하하하핳ㅎ



칙칙했던 우분투가 화려해지니 코딩할만 하겠네요 ㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎㅎ....

