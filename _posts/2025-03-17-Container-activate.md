---
title:  "[Trouble Shooting] Docker 컨테이너에서 conda 'activate' 안됨 / 오류"
excerpt: "컨테이너에서 conda env는 만들어졌지만, 'activate' 명령어가 되지 않는 경우 해결방법을 적었습니다."

toc : true
toc_sticky: true

header:
  teaser: /assets/images/container-activate.png
  
---

## 👀 문제 상황
**Docker 컨테이너** 내부에서 

![](https://github.com/user-attachments/assets/98638625-ae8e-42ec-bf1c-59492fa4c783)

이렇게 ``conda create -n {env_name}``을 사용하여 **가상환경**을 만들었습니다.

![Image](https://github.com/user-attachments/assets/ae99df66-eafa-4c10-a90e-0700e52d26f5)
``conda activate {env_name}``을 통해 가상환경을 **활성화** 시키려고 하면, 다음과 같이 **conda: errer: argument COMMAND: invalid choice** 에러가 뜹니다.

<br>

## 🔑 컨테이너 속 Command Invalid Choice 해결 방법
다음 방법을 **순서대로** 따라해주세요 : )
1. **``~/.bashrc``에 경로 추가**
```
echo 'export PATH="/opt/conda/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```
2. **``conda init`` 실행**
```
conda init bash
exec bash
```

<br>

## 💻 해결 방법 적용 후 결과
다음과 같이 ``conda activate`` 명령어가 문제 없이 사용되는 것을 확인할 수 있습니다.
![Image](https://github.com/user-attachments/assets/a787d0c2-ce1b-4da9-a8c9-179d23de4241)

<font style="color:hsl(27, 100%, 43%)">아 주 초 간 단 !</font>
<br>
