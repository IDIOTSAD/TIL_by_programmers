# 강의 영상

> * bgr 3개의 값 타입을 저장할 수 있는 변수 = Vec3b
> * uchar val[3]이 구성되어 있음.
> * at\<Vec3b>(y,x)\[0]으로 바로 접근하는 것과 v에 at\<Vec3b>(y,x)를 저장하고, v\[0]을 하는 것의 차이점
> * 접근을 매번 해야하는 것(find)과 저장된 변수에서 바로 접근이 되거나.
> * 따라서, 뒤에 있는 방법 변수를 저장하고 접근하는 것이 더욱 빠르다. = 하지만, 알아서 최적화를 해주기 때문에 아무렇게 써도 됨.
> * IMREAD_GRAYSCALE과 cvtColor를 이용하면, 다르게 나오는 경우가 있었음. = OpenSource 라서 버그나 잘못됐을 때 책임이 부족함.

> * RGB 색상을 그레이스케일로 변환
> * Y = 0.299R + 0.587G + 0.114B (간단하게 하면, r + g + b 에 3을 나눈거도 되기도 함 = 안쓰는게 좋음)
> * 장점 = 데이터 저장 용량 감소, 연산 처리 속도 향상
> * 단점 = 색상 정보 손실
> * 제일 많이 사용하는 매크로 함수 이용법

![image](https://user-images.githubusercontent.com/55529455/159624775-5751bebc-1ee2-4dc1-b3c1-5cbc00ddc3c9.png)

> * 색 공간 변환
> * 영상처리에서는 특정한 목적을 위해 RGB 색 공간을 HSV, YCrCb, Lab 등의 다른 색 공간으로 변환하여 처리 (컬러 스페이스, 컬러 모델)
> * OpenCV 색 공간 변환 방법: https://docs.opencv.org/master/de/d25/imgproc_color_conversions.html

![image](https://user-images.githubusercontent.com/55529455/159626059-b96a7ebc-a08d-4c25-a2df-a87a6c95064f.png)

> * RGB 색 공간
> * 빛의 삼원색인 R, G, B를 혼합해서 색상을 표현
> * TV&모니터, 카메라센서 bayer 필터, 비트맵

![image](https://user-images.githubusercontent.com/55529455/159628451-55ecc317-2779-4524-a9cd-d7835d2748ec.png)
![image](https://user-images.githubusercontent.com/55529455/159629058-183e3864-62d9-4635-b906-310d965ca67e.png)

> * 컬러 영상을 밝기 정보와 색 정보로 분할 = Cr, Cb 성분, Y 성분으로
> * White Balance (color temperature) = 사진을 찍었을 때, 흰색을 흰색답게 처리한 영상
> * 기능 파트가 문제가 생기면, 사진을 찍으려 할 때, 카메라가 꺼지는 것
> * 화질 파트가 문제가 생기면, 사진이 이상하게 찍히는 것
> * 기능 vs 화질 -> 화질이 더 중요함.

![image](https://user-images.githubusercontent.com/55529455/159638026-a569f0bd-c7c7-41e5-9d49-89b50cf80cf3.png)

> * 각각의 이퀄라이제이션에 대해서 다르게 나타남.
> * 밝기 성분에 대해서만 히스토그램 평활화 수행해야함.
> * Cr, Cb는 그대로 나둬야 하는 것이 포인트
> * 

