# 강의 요약

> * 자이카 카메라 활용
> * 카메라 = 1/3 CMOS OV2710 센서
> * 640p 120fps, 1080p 30fps
> * USB 비디오 클래스 UVC 1.1

> * 카메라 활용 사례

> * 카메라로 차선등을 찾아 자율주행 구현
> * 차선 찾아서 차선을 벗어나지 않고 주행
> * 사람을 찾아서 사람을 쫒아 주행
> * 앞차의 뒤를 보고 앞 차를 따라감

> * 카메라를 이용한 주변상황 인지
> * 전방 이동물체 인식 - 차량, 사람, 자전거 판단
> * 전방 고정물체 인식 - 교통표지판, 신호등, 정지선, 횡단보도, 언덕

> * 카메라 영상으로 자기 위치 파악 (Localization)
> * 앞에 펼쳐진 전경을 보고, 또는 지형지물을 봄
> * 지도 데이터와 비교하여 현재 차량 위치 파악

> * 카메라는 상하 좌우를 움직이도록 만들어짐. (격자 선을 이용하여 영상에 잡히는 영역을 조정함)

![image](https://user-images.githubusercontent.com/55529455/160541161-6df90246-4803-40f2-8b2c-51c458f7c7e0.png)
![image](https://user-images.githubusercontent.com/55529455/160541191-2a1272d1-7e38-4883-8afd-0cfd6e016ade.png)
![image](https://user-images.githubusercontent.com/55529455/160541239-558582d1-94fe-47b7-b417-68454f4bac56.png)
![image](https://user-images.githubusercontent.com/55529455/160541260-12ec0108-75d6-4237-a393-c5db7c261dee.png)
![image](https://user-images.githubusercontent.com/55529455/160541286-34ce2bf4-ab35-4a1c-b631-528133e6bef9.png)
![image](https://user-images.githubusercontent.com/55529455/160541308-9519005c-92d4-429f-8b32-37270c0a4ef5.png)

> * 패키지 생성
```
catkin_create_pkg my_cam std_msgs rospy
cd ~/catkin_ws/my_cam/
mkdir launch
```
> * launch 파일 생성

![image](https://user-images.githubusercontent.com/55529455/160541532-098515b3-10e7-4d0e-8a8d-6dd9a3a09a81.png)
![image](https://user-images.githubusercontent.com/55529455/160544118-cb66c201-089a-4f48-b477-46305eb0aa63.png)
![image](https://user-images.githubusercontent.com/55529455/160544138-1510ae6e-7f21-4e83-bd70-fc155b288cf6.png)
![image](https://user-images.githubusercontent.com/55529455/160544169-4aa28fbb-4dbe-4c3a-8282-c6a8446ce28b.png)

> * ROS 토픽의 저장
> * 카메라의 ROS 토픽을 저장했다가 나중에 사용 할 수 있음.
> * rosbag record -a (모든 토픽 저장, 멈추려면 ctrl + c)
> * rosbag record rosout xycar_imu (rosout, xycar_imu 토픽 저장)
> * rosbag record -O subset xycar_ultrasonic (xycar_ultrasonic 토픽을 subset.bag 파일로 저장)
> * rosbag info subset.bag (해당 bag 파일의 정보를 보여줌)

> * ROS 토픽의 재생
> * rosbag play \*.bag (bag 파일 재생)
> * rosbag play -r 2 \*.bag (2배속 재생)

> * bag 파일에서 특정 topic 추출
> * 재생시킨 후, 토픽만 골라서 rosbag record 수행, 마지막으로 info로 확인.

![image](https://user-images.githubusercontent.com/55529455/160544607-73823d03-4d11-4491-98ce-6ebdb94efa89.png)
> * 차선을 따라 주행하기
> * USB 카메라와 OpenCV를 이용하여 차선을 인식하고, 인식된 차선을 따라 스스로 주행 할 수 있는 자율 주행

> * 차선 추종 주행
> * 좌우 차선을 찾아내어 차선을 벗어나지 않게끔 주행하면 된다.
> * 카메라 입력으로 취득한 영상에서 적절한 영역을 잘라냄 (ROI) = 어디를 자를지 잘 정해야함.
> * 잘라낸 사진을 이진화를 통해서 영상을 분석함.
> * 우선 바깥에서 중앙으로 가면서 흰색 점을 찾고, 그 점 주위에 사각형을 쳐서 사각형 안에 있는 흰색점을 구한다. 일정 개수가 넘어가면 차선이라고 인지

> * 차선을 찾기 위한 작업
> * Image Read : 카메라 영상신호를 이미지로 읽기
> * GrayScale : 흑백 이미지로 구분
> * Gaussian Blur 노이즈 제거
> * HSV - Binary : HSV 기반으로 이진화 처리
> * ROI : 관심영역 자르기

> * 가우시안 블러 원리
> * 각 픽셀에 5x5 윈도우를 올려놓고, 그 영역 안의 포함되는 값을 모두 더함.
> * 이후, 25로 나누어 인접한 점들의 밝기의 산술 평균을 구하는 방법으로 노이즈를 제거
> * 윈도우의 크기를 크게 할 수록, 부드러운 blur를 얻게 됨.

> * 카메라 영상에서 차선 검출하기
> * 트랙 영상에서 특정 영역을 ROI로 지정하여 차선 위치를 검출
> * BGR -> HSV -> Binary
> * 검출된 차선을 녹색 사각형으로 표시하기
> * 이진화된 이미지를 BGR로 변환시켜 색상을 가지는 사각형이 표현될 수 있음.

> * ROI 지정
> * 동영상 파일의 프레임 크기 640 x 480
> * 세로 좌표 430 ~ 450 영역을 ROI로 지정
> * 가로 좌표 0 ~ 200과 440 ~ 640을 각각 왼쪽, 오른쪽 차선을 발견하기 위한 구건으로 설정
> * 이 좌표는 차선을 잘 잡아낼 수 있는 영역을 정하는 것으로 상황에 따라 달라짐.

![image](https://user-images.githubusercontent.com/55529455/160545759-cb9bb0c8-00d6-4e5d-8534-ecbb23d94d4f.png)

> * 영역 내 흰색 픽셀 개수를 기준으로 차선 인식
> * 녹색 사각형은 검출된 차선의 위치를 표시
> * 사각형 안의 흰 픽셀 수를 기준으로 검출 영역의 가로 x 세로 크기는 20 x 10
> * 위 200개, 픽셀 중, 160개 이상이 흰색이면 차선으로 간주
> * 검출을 위한 영역의 크기 및 차선 인식을 위한 흰색 픽셀 비율의 하한 값은 모두 변경 가능

![image](https://user-images.githubusercontent.com/55529455/160545958-ea6de821-de79-446c-8919-b5a421e66545.png)

> * 잘라낸 영역에서 한 픽셀씩 움직이면서 차선 찾기
> * 중앙에서 바깥으로 vs 왼쪽과 오른쪽 끝에서 중앙으로 가면서? = 정답은 후자.

## 실습 (명도차 기반 차선 인식주행)
> * 카메라로 촬영한 차량 전방의 도로 영상을 OpenCV를 이용하여 명도차 기반으로 차선을 찾고, 양쪽 차선의 위치를 따져서 핸들을 얼마나 꺽을지 결정
> * 카메라의 입력 프레임 취득
> * 얻어낸 영상데이터를 처리하여 차선 위치 결정 (색변환, 이진화, 관심영역 찾기)
> * 차선 검출 : 흰색 점들이 모여 있는 곳의 좌표를 계산 = 검출한 차선 위치에 도형(사각형)을 그려서 차선검출 결과의 확인에 이용
> * 차선 위치를 기준으로 조향각 결정 = 차선의 중앙을 차량이 달리도록
> * 결정한 조향각에 따라 조향 모터를 제어 = 모터제어 메시지 전송

> * 명도 대비만으로 차선을 검출하기 쉽지 않음.
> * 명도 하한을 ROI 전체의 평균을 기준으로 설정한다면?
> * 명도 기준의 인식과 윤관ㄱ선 추출을 함께 적용한다면?

> * 늘 양쪽 차선이 보이는 것은 아님.

![image](https://user-images.githubusercontent.com/55529455/160546656-3dfe7703-5654-4783-9929-addbe4e358f5.png)
![image](https://user-images.githubusercontent.com/55529455/160546685-ef153d1b-d5e1-4070-8233-5344f4dc13a1.png)

> * 카메라의 자세 조정
> * 카메라 자세를 정확하게 세팅할 때 사용 = 손으로 직접 세팅
> * 카메라 영상에 격자를 그려서 표시함. 스스로 정한 기준에 따라 카메라 자세를 잡음 (종료는 Ctrl + C)

> * 조향각 제어
> * 직선 차로 = 주로 빠르게 정면으로 직진
> * 곡선 차로 = 차로가 휘어진 방향으로 적절히 느리게 (차선이탈 방지)

> * 조향 제어 기법

![image](https://user-images.githubusercontent.com/55529455/160546904-aac9b7d8-a9f8-48db-8132-e616acf9154c.png)
![image](https://user-images.githubusercontent.com/55529455/160546939-edeb8320-8c2a-465b-ab6c-1a2e02a6904e.png)
![image](https://user-images.githubusercontent.com/55529455/160546963-aa224586-180e-4d4f-99c6-868d6fe46e47.png)
![image](https://user-images.githubusercontent.com/55529455/160546982-b743dd7e-f37a-45d4-9eda-436e676a4cca.png)

> * 영상에서 차선 찾아내기
> * 허프 변환을 이용한 차선 추출
> * grayscale - blur - canny edge - roi - hough transform - result로 구성

![image](https://user-images.githubusercontent.com/55529455/160547281-b7fdb822-051f-4ad7-acf0-208f13017cbe.png)
![image](https://user-images.githubusercontent.com/55529455/160547313-261f09ad-6db2-46f2-b575-304fb91c808d.png)
![image](https://user-images.githubusercontent.com/55529455/160547372-131617bb-5e1a-4a30-82aa-33f2d1743e97.png)
![image](https://user-images.githubusercontent.com/55529455/160547435-0df163c2-d1c0-4718-940c-f08b9607b511.png)
![image](https://user-images.githubusercontent.com/55529455/160547463-6f6bf754-31e9-495c-a5b3-c8cc1bd720a9.png)
![image](https://user-images.githubusercontent.com/55529455/160547542-65980819-78d5-4b73-9617-e90f011a6ccf.png)
![image](https://user-images.githubusercontent.com/55529455/160547599-ce06b5d6-886f-4cae-9065-a8cca051d949.png)
![image](https://user-images.githubusercontent.com/55529455/160547649-0c5090af-0653-4a22-a9a4-80406d573e12.png)
![image](https://user-images.githubusercontent.com/55529455/160547680-a1e0e2ef-69f1-41d4-8e3b-2ee5a2dec328.png)
![image](https://user-images.githubusercontent.com/55529455/160547724-cd42a2aa-e9f4-469a-8b67-aa2450e87a7e.png)
![image](https://user-images.githubusercontent.com/55529455/160547771-1ae8a8e1-b936-4eab-a807-b9fd05d36ff5.png)







