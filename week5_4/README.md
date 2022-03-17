# 1장 강의 요약

> * 특별히 언급하지 않는 한 그레이스케일 영상을 사용
> * 대부분의 컴퓨터 비전 (영상처리) 알고리즘이 그레이 스케일 영상을 사용함
> * 트루컬러를 쓸 경우 그레이스케일에 비해 용량이 3배가 되기 때문이다. - 시간소요가 3배가 걸림.

![image](https://user-images.githubusercontent.com/55529455/158735941-f7c8d0d9-93c6-479e-b620-157c6a32d8e5.png)

> * 영상의 화소 처리 기법
> * 화소 처리 (point processing)
> * 입력 영상의 특정 좌표 픽셀 값을 변경하여 출력 영상의 해당 좌표 픽셀값으로 설정하는 연산
> * 결과 영상의 픽셀 값이 정해진 범위(그레이스케일, 0-255)이 있어야 함.
> * 반전, 밝기 조절, 명암비 조절, 이잔화 등
> * dst(x,y) = f(src(x,y)) => (dst = 입력, src = 출력, x, y 좌표, 어떤 함수에 들어가서 출력 영상을 만들어냄. - 이 함수를 변환 함수라고 함.)

> * 밝기 조절
> * 영상 전체 밝기를 일괄적으로 밝게 만들거나 어둡게 만드는 연산
> * 0 ~ 255 범위를 +-50 씩 하여 밝기를 조절함.
> * 밝기 조절 수식 = dst(x,y) = src(x,y) + n (saturate 연산, limit 연산)

> * 소스코드

```
#include <iostream>
#include "opencv2/opencv.hpp"

using namespace std;
using namespace cv;

int main()
{
	Mat src = imread("lenna.bmp", IMREAD_GRAYSCALE);

	if (src.empty()) {
		cerr << "Image laod failed!" << endl;
		return -1;
	}

#if 0
	Mat dst = src + 50;
	// 자동으로 saturate를 해줌.
#else
	Mat dst(src.rows, src.cols, CV_8UC1, Scalar(0));

	for (int y = 0; y < src.rows; y++) {
		for (int x = 0; x < src.cols; x++) {
			int v = src.at<uchar>(y, x) - 50;
			if (v < 0) v = 0;
			dst.at<uchar>(y, x) = v;
			// dst.at<uchar>(y, x) = src.at<uchar>(y, x) + 50;
			// 이렇게 쓰면 생기는 문제점이 255 이상의 값은 0부터 다시 시작되기 때문에 문제가 됨.
			// uchar + int 연산으로 되기 때문에 int로 자료형이 변경되어 해당 문제가 생김.
			// 이를 해결하기 위해서 saturate를 해주어야 함. (포화 연산)
			/* 해결방법
			int v = src.at<uchar>(y, x) + 50;
			if (v > 255) v = 255;
			dst.at<uchar>(y, x) = v;
			
			* 빼기 연산
			int v = src.at<uchar>(y, x) - 50;
			if (v < 0) v = 0;
			dst.at<uchar>(y, x) = v;
			*/
		}
	}
#endif

	imshow("src", src);
	imshow("dst", dst);
	waitKey();
}
```
> * OpenCV 포화 연산 함수 = saturate_cast() 함수가 존재함.
> * saturate_cast<자료형>(값)으로 구성됨.

> * 해당 연산을 수행 할 때, cv::add 함수를 이용해도 된다.
> * 첫번째 영상, 두번째 영상(첫 번째 영상에서 덧셈 할 내용), 출력 영상, 마스크 파라메터로 구성됨.
> * add 연산은 매우 빠름. add 함수의 소요시간은 0.2~0.3의 시간이 걸리지만, 덧셈을 직접 구현 시 0.5~0.6 정도의 시간이 소요됨.
> * OpenCV는 멀티코어 프로그래밍이 되어있기 때문에, CPU 코어를 전부 사용함. (OpenCV 라이브러리)
> * 하지만, 직접 코드를 구현 하게 된다면, CPU 코어를 1개 쓰기 때문에 해당 결과가 나옴.

> * 영상의 반전
> * 영상 내의 모든 픽셀 값을 각각 그레이 스케일 최대값에서 뺸 값으로 설정
> * 밝은 픽셀은 어둡게, 어두운 픽셀은 밝게 변경하는 연산
> * 컬러 영상에 대해서는 각각 색상 성분에 대해 반전
> * 반전을 사용하는 이유는 대표적인 사례로 글씨 검출 (검은색 글씨에 하얀색 배경)
> * dst(x,y) = 255 - src(x,y)

> * 명암비(Contrast)
> * 밝은 곳과 어두운 곳 사이에 드러나는 밝기 정도의 차이
> * 컨트라스트, 대비
> * 밝기 정도의 차이가 높을 수록 좋음.
> * dst(x, y) = saturate(s \* src(x,y))
> > * dst(x, y) = src + (src-128) \* s => 255의 중앙값을 이용한 명암비 계산
> * 하지만, s값이 커질 수록, 명암 차이가 커지고, 이로 인해 명암의 차이가 없는 영상이 만들어지는 단점이 있다.
> * 따라서, 효과적인 명암비 조절 방법을 사용해야함.

![image](https://user-images.githubusercontent.com/55529455/158747370-de8f008b-b097-47a2-a12c-aec83e02f9d0.png)

> * 영상의 평균 밝기 m을 구하여 (m,m) 점을 지나는 직선을 변환함수로 사용
> * dst(x, y) = src + (src-m) \* s -> 평균값 이용

> * 히스토그램
> * 영상의 픽셀 값 분포를 그래프의 형태로 표현 한 것
> * 예를 들어 그레이 스케일 영상에서 각 그레이 스케일 값에 해당하는 픽셀의 개수를 구하고, 이를 막대 그래프의 형태로 표현

![image](https://user-images.githubusercontent.com/55529455/158749046-5ce85640-b00b-4101-aec6-6583596dfdbe.png)

> * 정규화된 히스토그램
> * 히스토그램으로 구한 각 픽셀의 개수를 영상 전체 픽셀 개수로 나누어 준 것
> * 해당 그레이 스케일 값을 갖는 픽셀이 나타날 확률을 의미함.
> * 일반 히스토그램은 정수, 정규화된 히스토그램은 실수로 표현이 됨. (정규화된 히스토그램을 다 더해주면 1, 히스토그램의 합은 전체 픽셀 개수)

![image](https://user-images.githubusercontent.com/55529455/158750724-245ab8fb-0bf9-4847-b0a4-b555f600d442.png)

