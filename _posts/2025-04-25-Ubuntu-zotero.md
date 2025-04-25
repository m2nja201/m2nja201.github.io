---
title:  "[Ubuntu] 간단하게 Ubuntu에 Zotero 최신버전 설치하기 (터미널 사용)"
excerpt: "Ubuntu에서 쉽고 빠르게 zotero 설치하는 방법에 대해 설명하였습니다."

toc : true
toc_sticky: true

categories:
  - Ubuntu

header:
  teaser: https://i.ibb.co/6RHXppmk/thumbnails-1.png
  
---

zotero download 페이지에 들어가면, ubuntu 프로그램 다운받는 버튼이 있는데, tar 파일이 다운로드 되더라구요..? 또 뭘 해줘야 한다고 해서, **간단하게 명령어로 다운**받는 방법을 소개하고자 합니다.

## 🦁 Zotero 설치 파일 다운로드
터미널에 들어가서 다음 명령어를 **순서대로** 입력해주세요.

```
curl -sL https://raw.githubusercontent.com/retorquere/zotero-deb/master/install.sh | sudo bash
sudo apt update
sudo apt install zotero
```

## 🦁 Zotero 설치 결과
아주 초간단으로 우분투에 zotero 설치하기 끝!
<center><img src="https://i.ibb.co/pv5KpzFH/image.png" width='80%' height='80%'></center>

### 참고 사이트
- [Zotero git hub](http://github.com/retorquere/zotero-deb)
