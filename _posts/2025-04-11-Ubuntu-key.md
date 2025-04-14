---
title:  "[Ubuntu] Ubuntu 24.04 LTS 한/영 키 사용 방법 (한글 입력 방법)"
excerpt: "우분투에서 한영키 전환하는 방법에 대해 설명드리겠습니다!"

toc : true
toc_sticky: true

categories:
  - Programming
  - Ubuntu

header:
  teaser: https://i.ibb.co/6RHXppmk/thumbnails-1.png
  
---

정말 똑~~~같이 따라해주시면 될 것 같습니다. 중간에 나오는 <strong>"Hangul"</strong>은 꼭 그대로 따라해주셔야 합니다. 그럼 아주 손쉽게 **한영키** 바꿀 수 있습니다 :) 

## ☝🏻 한글 패키지 설치

### 1. Setting - System - Region & Language 설정

<center><img src="https://i.ibb.co/hFGHLHXW/1.png" width='60%' height='60%'></center>

여기서 하단 **Your Account**의 <font style="color:hsl(27, 100%, 43%)">Language</font>에 들어갑니다.

<br>

### 2. Language에 들어온 후, ``Install/Remove Language`` 클릭

<center><img src="https://i.ibb.co/5X6MKdP5/2.png" width='60%' height='60%'></center>
<br>

### 3. ``Korean``을 찾아 ``Installed``에 체크 ✅

<center><img src="https://i.ibb.co/1t89K01S/3.png" width='60%' height='60%'></center>

**``apply``** 로 적용시켜줍니다.

<br>

### 4. Terminal 접속 - ``ibus-setup`` 명령어 입력하여 세팅 접속

<center><img src="https://i.ibb.co/YFG0MVF3/4.png" width='60%' height='60%'></center>

위 명령어를 입력하면 다음과 같은 화면이 뜹니다.

<center><img src="https://i.ibb.co/Y4w2Z1zT/5.png" width='60%' height='60%'></center>

여기서 **``add``** 를 눌러줍니다.

<center><img src="https://i.ibb.co/pBHGn6Xk/6.png" width='60%' height='60%'></center>

검색란에 ``korean``을 검색하면 <font style="color:hsl(27, 100%, 43%)">Hangul</font>이 나옵니다. 꼭 **``Hangul``** 을 선택하신 뒤, ``Add`` 눌러주셔야 합니다.
Korean으로 add하게 되면, 한영키 전환이 안돼요!!! ⭐️⭐️⭐️

<center><img src="https://i.ibb.co/nq1KQJFF/7.png" width='60%' height='60%'></center>
그럼 이렇게 Add가 됩니다!

<br>

## ✌🏻 한영키 전환 설정
### 1. Settings - Keyboard 설정

<center><img src="https://i.ibb.co/JWSsCLz7/8.png" width='60%' height='60%'></center>

설정 화면으로 들어갑니다. 여기서 **``Input Sources``** 의 **``Add Input Source``** 를 눌러주세요.

<br>

### 2. 입력 소스 설정

<center><img src="https://i.ibb.co/Z6rsZ5Cn/9.png" width='60%' height='60%'></center>

Korean이 바로 뜨지 않는 분들은 **``Other``** 를 꼭 눌러주세요!

이때 주의해야할 점은 <font style="color:hsl(27, 100%, 43%)">Korean(Hangul)</font> 을 눌러야 한다는 점!!!!

<br>

### 3. English는 삭제

<center><img src="https://i.ibb.co/j9cQSP8h/10.png" width='60%' height='60%'></center>

English 옆 미니 메뉴 버튼을 눌러서 **``Remove``** 를 선택해주세요.

<br>

### 4. 설정 확인 및 마무리

<center><img src="https://i.ibb.co/gZBkqY5Z/11.png" width='60%' height='60%'></center>

화면 우측 상단의 ``EN``을 눌렀을 때, 다음과 같이 **``Korean(Hangul)``** 이 뜨면 성공입니다. 한글을 사용하실 땐, <font style="color:hsl(27, 100%, 43%)">Hangul mode</font>를 on해주시면 되고,

키보드에서 <font style="color:hsl(27, 100%, 43%)">Shift + Spacebar</font>를 누르시면 스위치 On/off 할 필요 없이 **한/영 키 전환**이 됩니다!