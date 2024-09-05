---
title:  "[Ubuntu/Linux] /etc/passwd 수정 후 서버 접속 불가 문제 해결"
excerpt: "/etc/passwd 파일을 수정했을 때, 권한이 사라지는 문제와 서버 접속이 불가능한 문제를 해결하는 과정을 담고 있습니다."

toc: true
toc_sticky: true

categories:
  - Pages 
  - TroubleShooting

header:
  teaser: https://github.com/user-attachments/assets/7b8283f1-f352-4324-817f-b58513129245

---
나의 **대멘붕 상황**을 공유하며, 나와 같은 어리석은 짓은 하지 않도록 해결 방법을 나누고 싶었다...

## ⚠️ 문제 상황
- user에게 **superuser의 권한**을 주고 싶어서 여러 과정을 거친 후, 마지막으로 ``/etc/passwd`` 파일을 수정
  - ``/etc/passwd``의 구성은 다음과 같이 됨 ⇒ ``user_name:x:{user_id}:{group_id}:user comment:home directory:shell``
  - root와 동일한 권한을 주기 위해 **user id**와 **group id**를 ``0``으로 설정
  <center><img src="https://github.com/user-attachments/assets/c0cc02f5-9f8e-49f7-b15d-627c5b8fa593" width="90%"></center>
- ``/etc/passwd``를 수정한 이후로 일어난 문제
  - **sudo 명령어**를 사용했을 때 : ``sudo: you do not exist in the passwd database``
  - 잠시 후, **일반 명령어**를 사용했을 때 : ``Authentication denied``
  - 다른 shell로 **해당 서버를 접속**할 때 : 접속 불가
  - 서버 본체와 **모니터를 연결**하여 **직접 확인**한 결과 : 계정이 사라져있음(심장이 멎는 줄 알았다...)
- **내가 생각한 원인**
  - ``/etc/passwd``와 ``/etc/shadow`` 간의 관계가 파일이 수정되는 바람에 맞지 않아서 동작이 모두 멈춘 것 같다

## 🧯 해결 방법
### 첫 번째 방법 (본인은 이걸로 해결 못 함!)
``/etc/passwd-``와 ``/etc/shadow-``는 본 파일의 복사 파일로 해당 파일을 본 파일 위치에 다시 복사해주면 어긋났던 부분들이 괜찮아 진다... 라는 방법이었다. 
```
cp -p /etc/passwd- /etc/passwd 
cp -p /etc/shadow- /etc/shadow
```

애초에 서버에 들어가지지 않아서 해당 방법을 사용하지 못했다.

### 두 번째 방법
현재 서버 본체와 모니터를 연결하였을 때 우분투가 실행이 되며, 원래 있던 user 계정이 사라져있는 상태인 것이다!
1. **새로운 user 계정**을 만든다.
2. **terminal**에 들어가서 ``sudo su`` 명령어를 통해 **관리자 권한**으로 명령어 사용을 시작한다.
3. ``vi /etc/passwd``로 수정했던 passwd 파일을 연다.
4. 자신이 **수정했던 부분** (나같으면 user id와 group id)을 다시 원래대로 수정한다.
5. ``wq!``로 강제저장을 한다. (**이때 또 잘못된 부분은 없는지 꼭 확인..!**) 

생각보다 매우 간단하게 해결...
연구실 서버를 하나 통으로 날려버릴 뻔해서 너무 무서웠다...

## 💡 찾아본 그 외의 해결 방법
위 문제로도 해결이 되지 않았을 때 **최후의 수단**으로 준비해둔 방법들이다. 밑의 과정을 진행해본 적이 없어 자세히 적지 못하기 때문에 참고했던 **블로그 링크**를 함께 첨부하였다.

### Ubuntu 복구 모드 진입
1. PC 구동 후 ``shift`` 꾹 누르기
2. Advanced options for Ubuntu 클릭
3. **복구 모드** 클릭
4. ``mount -rw -o remount`` 명령어를 쳐서 root 명령어 사용
5. 위의 **해결 방법/두 번째 방법**을 진행

- **참고 링크**
  - https://mslee89.tistory.com/5

### Ubuntu 싱글 모드 진입
1. 부팅 시 아무 키를 눌러 커널모드로 진입
2. Ubuntu 부분에 커서를 두고 ``e``를 눌러 진입
3. ``ro``라고 되어 있는 부분을 ``rw single init=/bin/bash``로 변경한 후 ``ctrl+x``나 ``F10``을 눌러 부팅
4. ``mount -rw -o remount`` 명령어 사용
5. 위의 **해결 방법/두 번째 방법**을 진행

- **참고 링크**
  - https://platformengineer.tistory.com/47
  - https://kldp.org/node/33260
  - https://idchowto.com/ubuntu-22-04-%EC%8B%B1%EA%B8%80%EB%AA%A8%EB%93%9C%EB%A1%9C-%EC%A7%84%EC%9E%85%ED%95%98%EC%97%AC-%ED%8C%A8%EC%8A%A4%EC%9B%8C%EB%93%9C-%EB%B3%80%EA%B2%BD%ED%95%98%EA%B8%B0/