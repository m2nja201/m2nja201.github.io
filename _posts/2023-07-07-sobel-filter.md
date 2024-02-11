---
title:  "[openCV] Sobel Filter로 Edge 검출하기"
excerpt: "소벨 필터가 무엇인지, Sobel 함수는 어떻게 활용하는지, Edge 검출은 어떻게 하는지에 대한 게시글입니다."


toc : true
toc_sticky: true
---

## 👀 Sobel Filter
대표적인 **Edge 검출** 필터로, 
일반적으로 **가로방향**과 **세로방향**에 대한 edge 검출을 각각 수행한 뒤, **절대값의 합의 평균**으로 합성하여 최종 edge 값을 구한다.

![](https://velog.velcdn.com/images/m2nja201/post/974ec86b-e8db-4027-a518-307242f41e3e/image.png)

이때 **두 마스크의 합**이 **0이 되도록** 하면, 1로 정규화하는 과정은 필요 없다.

> 위 이미지에서 알 수 있듯이 **3 x 3 mask**에서는 행마다 3가지의 값이 있고, 이는 **이전값, 중간값, 다음값**으로 **중간값**을 기준으로 **이전값 ≤ 중간값 ≤ 다음값**을 만족하는 것을 볼 수 있다.

<br>

## 💻 Sobel Filter 사용

### 🔑 함수 사용
간단히 openCV를 통해 사용할 수 있는 **``Sobel`` 함수**가 있다.
```cpp
void cv::Sobel(
	InputArray	src,
    OutputArray dst,
    int			ddepth,
    int			dx,
    int			dy,
    int			ksize = 3,
    double		scale = 1,
    double		delta = 0,
    int			borderType = BORDER_DEFAULT)
```
이를 사용한 예제는 다음과 같다.
```cpp
Mat SobelFilter(Mat img) {
	Mat dstImg(img.size(), CV_8UC1);
	Mat sobelX, sobelY; // x방향과 y방향 mask를 각각 준비

	Sobel(img, sobelX, CV_8UC1, 1, 0); // 가로방향 sobel
	Sobel(img, sobelY, CV_8UC1, 0, 1); // 세로방향 sobel
	dstImg = (abs(sobelX) + abs(sobelY)) / 2; // 절대값 합의 평균
    
    return dstImg;
}

```

<br>

### 🔑 구현하여 사용
검색을 아무리 해도 위 **Sobel 함수로 원하는 대각을 설정**하는 예제를 찾지 못했다.
그래서 **직접 구현**하는 방법을 사용했다.

<br>

> #### 45도와 135도 대각 edge를 검출하는 Sobel Filter 구현
![](https://velog.velcdn.com/images/m2nja201/post/3cf33f84-010b-41f4-b6ba-8459d4f8d8c7/image.png)
```cpp
Mat mySobelFilter(Mat img) {
	int kernelX[3][3] = { -2, -1, 0,
						  -1,  0, 1,
						   0,  1, 2 }; // 가로방향 45도 sobel 마스크
	int kernelY[3][3] = { 0,  1,  2,
						  -1,  0,  1,
						  -2, -1,  0 }; // 세로방향 135도 sobel 마스크
	// mask 합이 0이 되므로 1로 정규화하는 과정 필요 x
	Mat dstImg(img.size(), CV_8UC1);
	uchar* srcData = img.data;
	uchar* dstData = dstImg.data;
	// 변수 지정
	int width = img.cols;
	int height = img.rows;
    // Data array에 값 입력
	for (int y = 0; y < height; y++) {
		for (int x = 0; x < width; x++) {
			dstData[y * width + x] = (abs(myKernelConv3x3(srcData, kernelX, x, y, width, height, 1)) +
								      abs(myKernelConv3x3(srcData, kernelY, x, y, width, height, 1))) / 2;
		}
	}
	return dstImg;
}
```
- 이때 ``img.data``는 1차원 배열인 것을 주의해야 한다.

<br>

사용한 **``myKernelConv3x3`` 함수**는 **마스크에 대한 convolution 처리**를 하는 함수이다.
```cpp
int myKernelConv3x3(uchar* arr, int kernel[][3], int x, int y, int width, int height, int ch, int BGR = 0) {
	int sum = 0;
	int sumKernel = 0;

	for (int j = -1; j <= 1; j++) {
		for (int i = -1; i <= 1; i++) {
			if ((y + j) >= 0 && (y + j) < height && (x + i) >= 0 && (x + i) < width) {
				if (ch == 1) {
					// 단일 채널이라면
					sum += arr[(y + j) * width + (x + i)] * kernel[i + 1][j + 1];
				}
				else if (ch == 3) {
					// 컬러 영상일 때
					sum += arr[(y + j) * width * 3 + (x + i) * 3 + BGR] + kernel[i + 1][j + 1];
				}
				sumKernel += kernel[i + 1][j + 1];
			}
		}
	}
	if (sumKernel != 0) {
		return sum / sumKernel; // 합이 1로 정규화되도록 하여 영상의 밝기 변화 방지
	}
	else return sum;
}
```

<br>

즉, 다음 코드에서 ``myKernelConv3x3(srcData, kernelX_Y, x, y, width, height, 1)``은 ``kernelX`` 혹은 ``kernelY``에 각 픽셀 ``(x, y)``에서의 edge값을 도출한 뒤 두개의 값을 더하여 평균을 구한 값을 **data**에 넣게 되는 것이다.
```cpp
for (int y = 0; y < height; y++) {
		for (int x = 0; x < width; x++) {
			dstData[y * width + x] = (abs(myKernelConv3x3(srcData, kernelX, x, y, width, height, 1)) +
								      abs(myKernelConv3x3(srcData, kernelY, x, y, width, height, 1))) / 2;
		}
	}
```
![](https://velog.velcdn.com/images/m2nja201/post/9613e25d-0c79-4825-82d3-f06cb85bccd4/image.png)

