---
title:  "[Ubuntu] Ubuntu 이미지 파일로 부팅 USB 만들기 (윈도우 부팅 USB, Refus)"
excerpt: "Window에서 Ubuntu 부팅 USB를 만드는 방법을 아주아주 깔끔하게 정리해봤습니다."

toc : true
toc_sticky: true

categories:
  - Programming
  - Ubuntu

header:
  teaser: https://i.ibb.co/6RHXppmk/thumbnails-1.png
  
---

## 📁 Ubuntu iso 파일 다운로드

**Ubuntu 다운로드 웹페이지** 접속 : [https://ubuntu.com/downloads/desktop](https://ubuntu.com/downloads/desktop)

<center><img src="https://i.ibb.co/xKGKt7BK/2025-04-11-3-05-40.png" width='700%' height='70%'></center>


먼저, <font style="color:hsl(0, 100.00%, 42.90%)">빨간색 네모 박스</font>가 있는 부분을 눌러 <strong>LTS 버전(장기 지원)</strong>을 설치합니다.

만약 안정적인 버전인 <strong>22.04 LTS</strong> 버전을 다운 받고 싶으시다면, <font style="color:#fdb603">노란색 네모 박스</font> 부분을 눌러주세요!

> **약간의 첨언😅** 
    : 너무 옛날 버전(20.04 LTS)를 사용하시면, **드라이버 설치 지원**이 안되는 것들이 간혹 있습니다. 저도 알고 싶지 않았습니다. ^^

<br>

## 💾 Refus 다운로드 및 부팅 USB 만들기

**Refus 프로그램** : 원하는 USB를 부팅이 가능한 부팅 USB로 만들어주는 프로그램

**주의할 점**은 <font style="color:hsl(27, 100%, 43%)">포맷가능한 USB</font>를 준비해야 한다는 점입니다. 부팅 USB로 만드는 과정에서 USB를 **포맷**합니다. 내용을 모두 **백업**한 후 사용해주세요.

### [1] Refus 웹페이지 접속 : [https://rufus.ie/ko/](https://rufus.ie/ko/)

밑으로 쭈욱 내리면 **다운로드**가 있습니다. 여기서 저는 **포터블** 버전으로 다운받아줬습니다. 


<center><img src="https://i.ibb.co/kVdr27Cr/2025-04-11-3-11-31.png" width='60%' height='60%'></center>


### [2] Refus 사용하여 부팅 USB 생성
다음과 같이 설정해줍니다.
- **장치** : 부팅 USB로 설정할 USB 장치
- **부트 선택** : Ubuntu에서 다운로드 받은 **iso 파일**을 **``선택``**을 눌러 지정
- **파티션 방식** : MBR
- **볼륨 레이블** : USB 이름으로 설정해줄 내용. 저는 설정 그대로 뒀습니다.

설정을 완료해주고 나면, 다음과 같이 **``시작``** 버튼을 눌러줍니다.


<center><img src="https://i.ibb.co/zhvTggmv/screenshot1-ko.png" width='45%' height='45%'></center>

<b>

만약 게이지가 초록색으로 꽉 차고, **``완료``** 상태가 되면 닫기로 꺼주시면 됩니다.

-> 만들기 끝.

