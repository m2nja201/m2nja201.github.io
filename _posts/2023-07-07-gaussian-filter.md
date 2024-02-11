---
title:  "[openCV] Gaussian Filter로 Blurring(블러링) 하기"
excerpt: "가우시안 필터가 무엇인지, Gaussian Blur 함수는 어떻게 활용하는지, 블러링은 어떻게 하는지에 대한 게시글입니다."

toc: true
toc_sticky: true

categories:
  - ComputerVision 
  - OpenCV

---

## 🌳 Gaussian Filter (가우시안 필터)
가우시안 분포 형태의 마스크로 **현재 화소와 가까울수록 가중치를 부여**한 mask를 사용하는 필터링 기법

<img src="https://velog.velcdn.com/images/m2nja201/post/4a47e8d9-266f-4998-80c5-41fe6c9efa3a/image.png" style="
    margin-top: 10px;
    margin-bottom: 0px;
">

<span style="display:inline-block; margin-top:-10px; padding-top : -10px; font-size:15px; color:gray; text-align:center; width:100vw">가우시안 분포 그래프</span>

<br>

### 👍 Gaussian Filter의 좋은점 ( vs 평균값 필터)
> #### **평균값 필터**란?
주변 화소와의 **산술 평균값**으로 mask를 사용하는 필터링 기법
→ 즉, 가까이 있는 픽셀과 멀리 있는 픽셀이 **모두 같은 가중치의 평균값**으로 계산되기 때문에 
   멀리 있는 픽셀(**본 픽셀과 관련성이 별로 없는 픽셀**)의 영향을 받을 수 있다.

**gaussian filter**는
- 멀리 있는 픽셀의 영향을 많이 받지 않는다.
- 더 자연스러운 블러 효과를 얻을 수 있다.

<br>

## 💻 openCV Gaussian Filter 사용
``` cpp
void cv::GaussianBlur 	(
		InputArray  	src,
		OutputArray  	dst,
		Size  			ksize,
		double  		sigmaX,
		double  		sigmaY = 0,
		int  			borderType = BORDER_DEFAULT 
	) 
```
``ksize`` 를 ``Size()`` 값을 사용하게 되면, **sigma** 값에 의해 결정된다.
- gray scale image는 6σ+1, true color image는 8σ+1의 크기로 결정된다.
- 이때 **sigma 값**을 증가시킬 수록 **블러링 효과**는 더 커진다.


9 x 9 사이즈의 mask를 사용한다면, 다음과 같이 **GaussianFilter**를 사용할 수 있다. (``cpp``)
``` cpp
Mat myGaussianFilter(Mat img) {
	Mat dstImg(img.size(), CV_8UC3);
	GaussianBlur(img, dstImg, Size(9, 9), 0); // 마스크의 크기는 9x9로 지정하여 자체적으로 마스크 생성 후 연산

	return dstImg;
}
```
자체적으로 구현을 하여 사용할 수 있으나, 실사용에선 **``GaussainBlur`` 함수**를 사용하기에 함수 설명만 업로드 하였다! 

<br>

### 📊 Gaussian Filter 적용 전과 후, histogram 비교
<img src="https://velog.velcdn.com/images/m2nja201/post/20292ab9-96a1-4fb8-95af-1e78b1704f6b/image.png" style="
    margin-top: 10px;
    margin-bottom: 0px;
">

<div style="margin-top:-10px; padding-top : -10px; font-size:15px; color:gray; text-align:center;">상단 : 이미지 원본 / 하단 : 가우시안 필터 적용 후</div>

Gaussian Filter를 적용하면서 **히스토그램의 분포 균형**이 조금 더 개선되었다.

<br>

### 💡 Sigma 값에 따른 Gaussian Blur 효과 정도 비교
``` cpp
Mat origin = imread("C:\\cv_img\\gear.jpg", 0);
	imshow("origin", origin);

	Mat blured;
	for (int sigma = 1; sigma <= 5; sigma++) {
		GaussianBlur(origin, blured, Size(), (double)sigma);

		imshow(to_string(sigma), blured);
		waitKey(0);
	}
```
위의 코드를 사용하여 이미지 확인
<img src="https://velog.velcdn.com/images/m2nja201/post/2ac892f9-81cf-4e36-940a-9708b4110dc0/image.png" style="
    margin-top: 10px;
    margin-bottom: 0px;
">
**sigma의 값**이 **커질**수록 **blur 효과**도 **커진다**는 것을 확인할 수 있다.

<br>

### 🪄 Noise가 있는 이미지에 Gaussian Filter 적용
<img src="https://velog.velcdn.com/images/m2nja201/post/02e6d64c-b966-47ed-97dd-bdd825df3a1d/image.png" style="
    margin-top: 10px;
    margin-bottom: 0px;
">

<div style="margin-top:-10px; padding-top : -10px; font-size:15px; color:gray; text-align:center;">좌측 : 이미지에 노이즈 추가 / 우측 : 가우시안 필터 적용 후</div>

Gaussian Filter를 적용하면서 **Noise가 감소**되었고, **블러링**되었다.