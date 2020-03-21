---
layout: post
title : "우분투 한글 입력기, 한영키 사용 (UIM)"
excerpt : "간단!"
date : 2020-03-22-03:34
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

처음에는 iBus를 사용하고 있었는데 크롬, 팀뷰어 등등 한글 입력이 어느순간 되지 않아 UIM을 사용하고 있습니다.



지금까지는 불편한 점도 없고 문제도 없어 잘 쓰는 중입니다!


---

<br/>

## UIM 설치

<br/>

```shell
$ sudo apt install uim
```

---
<br/>

## 설정 입력소스

<br/>

설치 후 설정에 가서 입력 소스를 영어(미국)만 남겨놓습니다.

<br/>

![](https://user-images.githubusercontent.com/57852139/77234640-6beadb00-6bf3-11ea-89f0-571481c93a96.png)


---

<br/>

## 언어 지원 입력기 변경

<br/>

그 다음 언어 지원에서 키보드 입력기를 uim로 변경합니다.

아이콘 테마를 적용해서 아이콘 모양은 다릅니다.

<br/>

![](https://user-images.githubusercontent.com/57852139/77235127-a43fe880-6bf6-11ea-9af2-8a4b38a11e1c.png)


<br/>


![](https://user-images.githubusercontent.com/57852139/77234974-93db3e00-6bf5-11ea-9647-73fa9f276817.png)


---

<br/>

## UIM 입력기 설정

<br/>

UIM 입력기 설정으로 갑니다.



<br/>



![](https://user-images.githubusercontent.com/57852139/77234794-87a2b100-6bf4-11ea-9285-c2c119a44bc2.png)





<br/>



디폴트 입력기를 벼루로 설정해주고 사용되는 입력기를 벼루만 남겨둡니다.

<br/>

![](https://user-images.githubusercontent.com/57852139/77235042-faf8f280-6bf5-11ea-8a85-c6218278e784.png)



<br/>



한영 전환 키와 한자 키를 설정해줍니다.

<br/>

![](https://user-images.githubusercontent.com/57852139/77235435-f4b84580-6bf8-11ea-90ce-08661fbd746a.png)
<br/>

근데 아직 한영키를 누르면 Alt키로 인식될겁니다. 제대로 인식되도록 설정하겠습니다.

<br/>

---

<br/>


## 한영키 인식

<br/>

gnome-tweak-tool (기능 개선)에서 설정해주겠습니다.

<br/>

![](https://user-images.githubusercontent.com/57852139/77235175-fbde5400-6bf6-11ea-8034-27242a8208f6.png)

<br/>

![](https://user-images.githubusercontent.com/57852139/77235206-347e2d80-6bf7-11ea-9fc9-c4d1a09a1d79.png)

<br/>

추가 배치 옵션을 클릭합니다.

<br/>

![](https://user-images.githubusercontent.com/57852139/77235223-5d062780-6bf7-11ea-9ef2-4566ef47b146.png)

<br/>

저기에 체크를 한 뒤 재부팅을 해주시면 인식이 될겁니다.

그 다음에 다시 입력기에서 설정해주시면 hangul로 제대로 인식됩니다.

---

<br/>

원래는 xmodmap으로 했었는데 재부팅할 때마다 다시 설정해야해서 altwin에서 설정해줬었습니다.

어쩌다보니 이 방법을 해봤는데 altwin 설정에서 안되던 한자 키도 적용이 되어 이 방법으로 하는 중입니다.

<br/>

다 설정한 뒤 재부팅을 해주시면 한영 전환이 잘 됩니다!!