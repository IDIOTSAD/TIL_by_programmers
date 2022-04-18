# 강의 요약

> Perception - Localization - Path planning - Control로 자율주행은 구성되어 있음.

> Perception
> 컴퓨터 비전 - 외부영상의 픽셀값으로 신호로 처리
> 센서 퓨전 - 카메라를 제외한 여러가지 센서 (라이다, 레이더)로 거리 등을 값을 받아와 외부 상황에 대해서 처리

> Localization - 내 차가 그 물체와 어느정도 위치에 있고, 라인을 따서 차 중심으로 어디에 있는지 매핑하는 것.

> Path Planning - 내 차 기준으로 맵을 만들었을 때, 주행 상황을 설계하는 것

> Control - 모든 정보에 대한 최종 결정(핸들, 엑셀, 브레이크)을 하여 차량을 움직이는 것.

> 센서의 종류
> 멀티 카메라, 레이더, 라이다
> 멀티 카메라 하는 이유 = 카메라의 사각지대가 존재해서는 안됨.
> 라이다 = 신호를 받아서 거리차를 재기 위해서

> 레이더 vs 라이다
> 레이더 = 라디오파를 사용한 무선감지 및 거리측정. 정밀도는 낮지만, 가격이 저렴
> 라이다 = 적외선 펄스를 사용한 물체감지 및 거리측정. 정밀도 높으며 가격이 비쌈

> 퍼셉션의 활용
> ADAS = 운전자 보조 시스템
> Parking assistance = 주차 보조 시스템

> 퍼셉션의 종류
> Classification (분류) - 무엇인지를 분류하는 것.
> Object detection (객체 인식) - 각 객체에 클래스를 매겨 바운딩 박스를 그려 분류하는 것
> semanic segmentation (군집화) - 픽셀값을 기준으로 모두 분류하는 것
> Instance segmentation (객체 군집화) - 픽셀값을 기준으로 원하는 객체만 분류하는 것
> Depth/Distance estimation - 각 객체간의 거리 관계를 추종
> Object tracking - detection의 결과를 기준으로 객체의 프레임의 결과를 인덱스를 부여하여 이전 인덱스와 같은지 구분

> Image Classification
> 어떤 이미지에 대해서 사전에 정의된 클래스 A인지 결과를 내는 것
> 딥러닝 모델을 통해서 결과가 나옴 -> 0.9 이런식으로 정확도
> Cat, Dog 2가지 레이블이 있다면, 고양이가 이미지가 들어가면 Cat 0.8 Dog 0.2 이런식으로 나옴

> 가장 많이 사용하는 모델은 CNN
> CNN (Convolutional Neural Network) - 이미지 처리에 특화 되어있는 네트워크
> RNN - 위성 처리에 특화
> RELU - 활성함수
> Pooling - 이미지를 줄이는 작업
> Flatten - 기하학적인 정보가 1자로 됨. Fully Connected로 연결하고 Softmax 값으로 클래스에 주어진 값을 봄.

> Classificatin History
> 2012 ImageNet
> 전통적인 CV 방식으로 하다가, Deep Learning으로 넘어가면서 70%의 정확성이 90%까지 올라감.
> LeNet5 - AlexNet - VGGNet - GoogleNet - ResNet
> https://paperswithcode.com
 
![image](https://user-images.githubusercontent.com/55529455/163766178-9f72b343-3366-409a-94ea-ea45cc762f7a.png)
![image](https://user-images.githubusercontent.com/55529455/163766207-5fa43e6f-42b5-401e-954e-45a634fcdc79.png)
![image](https://user-images.githubusercontent.com/55529455/163766222-769dca91-81f1-4545-97fb-8463536c3fec.png)
![image](https://user-images.githubusercontent.com/55529455/163766251-f2f7a67d-ae61-4aec-b9fe-c75a972c2aeb.png)
![image](https://user-images.githubusercontent.com/55529455/163766292-ae432635-9f50-4f5f-94aa-2457f1ffc599.png)
![image](https://user-images.githubusercontent.com/55529455/163766308-692853a9-8cb3-41ab-a7fa-1af3212047db.png)




















