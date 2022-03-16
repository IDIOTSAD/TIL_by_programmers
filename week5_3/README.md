# 1장 요약 (카메라와 동영상 처리)
> * VideoCapture 클래스
> * OpenCV에서는 카메라와 동영상으로부터 프레임을 받아오는 작업을 VideoCapture 클래스 하나로 처리함
> * 일단 카메라와 동영상을 여는 작업이 수행되면, 이후에는 매 프레임을 받아오는 공통의 작업을 수행

![image](https://user-images.githubusercontent.com/55529455/158538259-de9eebea-1574-46a7-bc56-200fb590d7a9.png)
![image](https://user-images.githubusercontent.com/55529455/158538301-bf847964-bbb0-4988-abde-923a5ba5d0de.png)
![image](https://user-images.githubusercontent.com/55529455/158538349-7a5de22d-5eb2-4545-abf0-4536c728e94d.png)
![image](https://user-images.githubusercontent.com/55529455/158538389-8d8c304a-4865-431c-ab4f-79b48fb58530.png)
![image](https://user-images.githubusercontent.com/55529455/158538576-7685da77-ec2d-4e2b-80c0-92ce1d620994.png)

> * VideoWriter 클래스
> * OpenCV는 일련의 정지 영상을 동영상 파일로 저장 할 수 있는 VideoWriter 클래스를 지원함.

![image](https://user-images.githubusercontent.com/55529455/158538841-14e45a15-17a8-484c-b054-f1637deb7e98.png)

> * 카메라 입력을 동영상 파일로 저장하는 예제 코드

![image](https://user-images.githubusercontent.com/55529455/158538935-b2781aa3-f4f8-4ce3-bd7a-9a47153e5ba1.png)

# 2장 요약 (OpenCV 그리기 함수)
> * OpenCV 주요 그리기 함수

![image](https://user-images.githubusercontent.com/55529455/158548668-bdc60403-b5a6-4d6b-918f-5d5f485ccf63.png)
![image](https://user-images.githubusercontent.com/55529455/158548762-7c7cc0cb-c684-436f-adb1-899013dd7ac1.png)
![image](https://user-images.githubusercontent.com/55529455/158549309-f666b16a-6756-4d6a-a7ab-2d7b23aabc38.png)
![image](https://user-images.githubusercontent.com/55529455/158549339-77b347e4-5e8b-45fb-a6ae-d5789c1dd2ab.png)
![image](https://user-images.githubusercontent.com/55529455/158549371-bc888810-435c-4956-bbc3-ad34e36a03d0.png)
![image](https://user-images.githubusercontent.com/55529455/158549443-4f211bc3-a4af-4fa3-9d4a-993aa284d3dd.png)

> * 예제 코드 (차선을 그리고 프레임 번호를 화면에 출력)

![image](https://user-images.githubusercontent.com/55529455/158549543-e39a3830-08ad-4ff4-9434-ea93fcd289c7.png)

# 3장 요약 (이벤트 처리하기)
> * 키보드 입력 대기

![image](https://user-images.githubusercontent.com/55529455/158550317-21ad407a-2418-4021-98b3-7e32daff93ee.png)

> * 마우스 이벤트 처리하기

![image](https://user-images.githubusercontent.com/55529455/158550389-f933a388-9d02-4dcb-a3c6-21385cb064aa.png)

> * 마우스 콜백함수의 이벤트의 플래그

![image](https://user-images.githubusercontent.com/55529455/158550463-01de5b9b-ae06-4f75-8a51-731415a74b68.png)

> * 키보드, 마우스 동작 여부를 확인 할 때, flags에서 == 가 아닌, & 연산을 통한 비트 연산자 비교로 하는 것이 일반적인 작성법임.
> * ==를 할 경우에는, 여러 동작을 한꺼번에 할 때 동작이 제대로 되지 않는 것을 확인 할 수 있음.
> * & 연산을 통해서 여러 동작 중, 해당 동작이 동작하는지에 대한 비트 마스크를 수행하는 것임.
> * 마우스를 이용해서 그림을 그리고 싶을 때, 해당 좌표에 점이나 원을 그리는 것을 하는 것이 아니라 이전 좌표와 현재좌표와의 거리에 직선을 긋는 것이 훨신 좋음.

> * 트랙바 = 영상 출력 창에 부착되어, 프로그램 동작 중에 사용자가 지정된 범위 안의 값을 선택할 수 있는 GUI
> * 슬라이더 컨트롤이 있음.

> * 트랙바 생성 함수

![image](https://user-images.githubusercontent.com/55529455/158551534-75f50a22-b5eb-471a-bd5b-10e8bdfad53f.png)


# 4장 요약 (유용한 OpenCV 함수)
> * 행렬의 합, 평균, 최댓값/최소값 구하기

![image](https://user-images.githubusercontent.com/55529455/158552751-13093fe4-0c24-425e-b344-c2804862fe6f.png)
![image](https://user-images.githubusercontent.com/55529455/158553908-520b6ee3-28fa-4bac-8895-ecb9bb9ac825.png)
![image](https://user-images.githubusercontent.com/55529455/158553998-4e023dc0-4e97-40d5-9130-08683ac907e9.png)

> * 평균에서 그레이 스케일이 아닌 경우에는(트루컬러), m\[3] 부분에서는 0이 채워지는 점이 있다.

> * 영상의 속성 변환

![image](https://user-images.githubusercontent.com/55529455/158554349-81cd3d7d-4d0b-4419-a219-180014e06d94.png)
![image](https://user-images.githubusercontent.com/55529455/158554411-5f0633a9-d367-4cd9-9900-b36157d801d7.png)
![image](https://user-images.githubusercontent.com/55529455/158554521-d959f391-b3b4-4d75-8feb-7a6eb0ce6ea0.png)
![image](https://user-images.githubusercontent.com/55529455/158555922-35e765a4-4e19-40b7-aa01-fee558b07c7b.png)
![image](https://user-images.githubusercontent.com/55529455/158555967-9f2631d0-2e24-4fe1-912d-1f83428bb361.png)
![image](https://user-images.githubusercontent.com/55529455/158556034-5693baa3-7ed7-4ef3-b0a5-8d6aab07ca1a.png)

# 5장 요약 (유용한 OpenCV 함수)
> * 연산 시간 측정
> * 대부분의 영상처리 시스템은 대용량 영상 데이터를 다루고 복잡한 알고리즘 연산을 사용
> * 영사어리 시스템 각 단계에서 소요되는 연산 시간을 측정하고 시간이 오래 걸리는 부분을 찾아 계산하는 시스템 최적화 작업이 필수
> * 그러므로 OpenCV에서도 연산 시간 측정을 위한 함수를 지원

> * 기본적인 연산 시간 측정 방법
```
int64 t1 = getTickCount();
my_func();
int64 t2 = getTickCount();
double ms = (t2 - t1) * 1000 / getTickFrequency();
```
> * 연산 시간 측정은 릴리즈 모드에서 수행해야함 (g++의 경우, -O2 옵션을 사용)

> * TickMeter 클래스
> * 연산 시간 측정을 위한 직관적인 인터페이스 제공
> * 클래스 내부에서 getTickCount()와 getTickFrequency() 함수를 조합하여 시간을 측정함.
> * start, stop, reset 함수도 존재.

![image](https://user-images.githubusercontent.com/55529455/158561512-c63bd346-eb2d-4d74-8b9b-514c393eb76d.png)
> * 관심영역(ROI) - Region of Interest
> * 영상에서 특정 연산을 수행하고자 하는 임의의 부분 영역

> * 마스크 연산
> * OpenCV에서는 일부 함수에 대해 ROI연산을 지원하고, 이 때, 마스크 영상을 인자로 함께 전달해야함. (copyTo, calcHist, bitwise_or, matchTemplate)
> * 마스크 영상은 CV_8UC1 그레이스케일 영상
> * 마스크 영상의 픽셀 값이 0이 아닌 위치에서만 연산 수행됨. - 보통 마스크 영상으로는 0 또는 255로 구성된 이진영상(바이너리 이미지)를 사용.

![image](https://user-images.githubusercontent.com/55529455/158561880-87a649d4-669b-481d-9fb1-95c524b4bb37.png)
![image](https://user-images.githubusercontent.com/55529455/158561926-c851c947-0000-4297-88e3-4197b47d73bd.png)

> * 이 때, 트루 컬러의 채널 중 (b,g,r,a) a 부분의 알파부분이 마스크 역할을 수행 할 수 있음.

