#  강의 요약

### 자율주행의 정의
* 운전자의 개입(조작)없이 목적지까지 차량 스스로 움직이는 기술 - 차량은 차, 비행기 등 다양함.
* Autonomous Driving, Autonomous Vehicle, Self Driving Car 등 다양한 용어로 불림 - 커뮤니케이션을 위해 정확한 용어 필수

### 자율주행 기술 구성 요소
* 센서로 부터 입력받고, 다양한 기술을 통해 데이터를 생성하고, 차량으로 출력함.
* Perception = 자율주행 차량의 주행환경에 대한 다양한 정보를 인지하는 기술
* Localization = 자율주행 차량의 현재 위치를 추정하는 기술 - GPS, 가장 중요한 기술 (좋은 구현을 위해서는 퍼셉션이 중요해짐)
* Planning = 자율주행 차량의 주행 환경, 위치 정보를 바탕으로 주행하는데 필요한 요소(경로, 판단, ...)를 생성&결정하는 기술 (패스 플래닝, 미스 플래닝, 디시전 플래닝)
* 패스 플래닝 - 자율주행의 주행경로를 결정하는 기술 - 글로벌 패스 플래닝, 로컬 패스 플래닝
* 미션 플래닝 - 주행 환경에 맞는 적절한 상호작용을 생성하는 기술
* 디시젼 메이킹 - 미션 플래닝에서 생성한 선택지 중에서 가장 적합한 선택을 하는 기술
* Control = 자율주행 차량이 원활한 주행을 할 수 있도록 차량을 제어하는 기술 (횡방향, 종방향 제어)

###  Perception
* 자율주행 차량의 주행 환경 정보를 인지한다.
* 다양한 센서(비전, 라이다, 레이더)를 사용하여 주행에 필요한 정보(장애물, 교통신호 등)을 인식한다.
* 인식된 다양한 정보로부터 자율주행 차량에 영향을 미칠 요소를 분석하고 측정하여, 환경을 이해한다.

### Localization
* 자율주행 차량의 현재 위치를 파악하기 위해, 크게 두 가지 방법
* GNSS 기반의 GLobal Position을 추정하는 방법 -> GPS / INS(&IMU) Fusion, GPS RTK
* 다른 센서 또는 데이터로부터 차량의 Global Position을 추정하는 방법 -> SLAM, Map Matching

### Planning
* Planning의 대표적인 예시로, 자율주행 차량의 경로 계획 (Path planning)이 있음.
* 네비게이션과 같이, 현재 위치로부터 목적지까지 도로 단위의 경로를 결정하는 방법 - Global Path planning
* 현재 주행환경에서 원활한/안전한 주행을 위한 차선 단위의 경로를 결정하는 방법 - Local Path Planning

### Control
* 차량에 인가된 목표 값(Desired Value)를 만족하기 위한 차량의 요소를 제어하는 기술
* 자동차의 경우, 차량의 (속도, 가속도, 순간 가속도)와 스티어링을 제어한다.
* 제어 대상의 Dynamics를 분석하고, 주행환경과의 상호 작용을 통해 차량 안정성을 제어한다.

### 시스템 아키텍처
```
* 카메라 - 시각 정보
* GPS - lon, lat 정보 제공
* IMU - 가속도, 차량의 방향 제공
* Encoders - 차량의 바퀴가 굴러가는 정도 정보 제공
```
* 지도의 정보를 통해서 Global Planner를 세울 수 있고, 세운 결과를 WayPoint Position decision 정보를 넘김.
* 센서의 정보를 받아 퍼셉션에서 정리하고, 그 결과를 Obstacle detection, Waypoint Posision decision 등에게 정보를 넘김.
* WayPoint가 정해졌다면, 그 안에서의 Local Planning을 수행함.
* Obstacle detection에서 장애물이 감지가 된다면, Collision Avoidance를 통해 Local Planning을 다시 계획함.
* 센서의 정보로도 Self Localization이 가능함.

![image](https://user-images.githubusercontent.com/55529455/166187444-2650ac10-44ff-400c-99b6-13a4079778a9.png)
![image](https://user-images.githubusercontent.com/55529455/166187806-d862be26-7ef4-4581-8868-65a390f6d66b.png)
![image](https://user-images.githubusercontent.com/55529455/166192363-b5b8a8b4-0066-4f6f-9f28-3d1ef830db7a.png)
![image](https://user-images.githubusercontent.com/55529455/166192377-041b4a3b-3a68-4c11-b1fd-13b946931fcc.png)
![image](https://user-images.githubusercontent.com/55529455/166192735-1a6b493a-a197-4e4a-9d64-05fc76d7a67c.png)
![image](https://user-images.githubusercontent.com/55529455/166192824-ffe0d633-cf24-48d8-a501-ad5da0968e57.png)

### 자율주행의 두가지 갈래
* 1. 웨이모
* 정밀지도(HD Map)을 기반으로 하는 자율주행 
* LIDAR 기반 자율주행

* 2. 테슬라, 모빌아이
* 비 정밀지도 기반 자율주행
* VISION 기반 자율주행

![image](https://user-images.githubusercontent.com/55529455/166193707-b0a6eab2-4f8b-4ec8-90c0-534772fbd733.png)

### HD Map vs Navigation Map
* 정밀지도
* HD(High Definition) Map으로 자율주행에 필요한 많은 사전 정보를 지도로 만듦.
* HD Map을 만드는 회사마다 구체적인 정의, 데이터가 조금씩 다르며 개발이 진행중

* HD Map은 차선 단위로 지도로 높은 정밀도, 다양한 정보를 제공함. 그러나, 지도 제작이 어렵고 비싸다는 단점이 있음.
* 일반적인 네비게이션에서 사용하는 지도는 Navigation Map.

### HD Map 제작 방법
* MMS(Mobile Mapping System) 고가의 장비를 장착한 데이터 취득 차량을 이용한다.
* 누적된 LAS(LAser) 데이터를 이용하여 필요한 데이터 요소를 추출&경량화 작업을 수행한다.

### Mobileye & tesla
* HD Map은 자율주행에 필요한 다양한 정보, 정확한 지도 데이터를 제공하는 장점이 있지만, 지도 제작과 유지보수가 어려운 단점이 있다.

* Mobileye 기술
* Road Experence Manager - 자율주행에 필요한 카메라 기반 비전 기술을 사용함. - 도로에서 사용할 수 있는 정보를 습득
* 해당 기술을 사용하는 다양한 유저로부터 많은 데이터를 누적하여 쌓는다. - 이를 정규화 시켜서 정밀지도처럼 만든다.

* tesla 기술 - 많은 카메라를 사용함
* Vector space - 다양한 카메라 사용하여 차선을 다방면으로 보고 하나의 차선이라고 인지하는 것
* OTA - 자동차와 서버의 무선 통신
* 모빌아이처럼 다양한 차량의 데이터를 통합하여 하나의 지도를 만들 수 있게 됨.
* 뉴럴 랜더링을 통해서 환경의 변화를 주어 자체적으로 학습한다고 함.

### Perception
* 카메라, 라이다, 레이더를 사용함.
* 주행 환경에 대한 데이터를 생성함.
* 다양한 특징을 가지는 센서를 사용, 센서의 고유환 특징을 활용하여 종합적인 정보를 추정
* Detection, Segmentation, Tracking, Prediction, 3d pose estimation, sensor fusion, acceleration 등의 기술이 있음.

### Detection
* vision, lidar, rader 등 다양한 센서를 활용하여 주행환경에 존재하는 특정 객체를 검출
* vision 기반의 2d image object detection, lidar를 통한 3d point cloud object detection 등이 있음.
* 최근 vision 기반의 3d object detection을 검출하려는 노력이 있음.

### segmentation
* 객체의 형태를 분할하는 기법, bounding box와 결과가 다름.
* vision, point cloud 등 다양한 센서를 활용함.
* classification, classification + localization은 single object 구분 기법
* object detection, instance segmentation은 multiple object 구분 기법
* object detection, instance segmentation의 차이점은 segmentation은 배경을 검출하지 않는다는 점이 있다.
* 클래스끼리 묶어서 표현하는 것이 segmentation, 라이다나 레이더에서도 가능함.

### Tracking
* 검출한 객체의 고유한 ID를 부여하고, 해당 객체가 동일한 객체임을 추적하는 기술
* 다중 객체를 추적하는 Mutiple Object Tracking(MOT)와, 단일 객체를 추적하는 Single Object Tracking(SOT)으로 구분한다.
* Tracker와 Detector와 추종하는 것이 다르다. - 해당 부분이 비교했을 때, 정확도가 높으면 동일한 객체가 지속적인 움직임을 하고 있다고 판단

### Prediction
* tracking과 유사함 - predection은 다양한 센서를 활용할 수 있음. tracking은 입려되는 센서에 따라 tracker가 붙음.
* 객체의 현재까지의 움직임과 객체의 고유한 특징 등 다양한 정보를 바탕으로 객체의 미래 움직임을 추정함
* Multimodal Trajectory Prediction이란 키워드로 활발한 연구가 진행중
* 사람같은 경우는 어디로 갈지 예측하기 어렵지만, 자동차의 경우는 전진 후진과 스티어링의 움직임만으로 제어하므로 예측할 수 있음.

### 3D POSE Estimation
* 객체를 인식하는것 뿐만 아니라, 객체의 정확한 위치를 추종하는 것.
* Vision의 Geometry 정보를 사용하는 방법과 위치정보를 획득할 수 있는 다른 센서와의 데이터 융합 방법으로 구분함.
* Multiple View Geometry 분야의 기술을 사용함, LiDAR 센서의 입력데이터는 3차원 위치 정보임.

### Camera vs LiDAR
* LiDAR는 객체를 구분할 수 없지만, 위치 정보를 획득할 수 있음. - x, y, z, intensity(반사율)의 데이터로 구성됨.
* Camera는 객체의 위치 정보를 획득할 수 없지만, 대상이 무엇인지 구별할 수 있음. - w, h, r, g, b의 데이터로 구성됨.

### Sensor Fusion
* 이처럼 각 센서는 고유한 장/단점이 있으므로, 유의미한 정보를 획득하기 위해서 센서 데이터를 융합하는 Sensor Fusion(Calibration) 방법을 사용함.
* camera로 검출된 객체를 lidar의 위치 데이터와 합쳐서 객체의 위치를 파악할 수 있게 됨.
* GPS, IMU로도 가능함. 위치와 가속도를 이용하여 가속도를 미분하여 속도를 얻고, 위치를 적분하여 속도를 얻어 정보를 이용함.

### Acceleration - 딥러닝, 머신러닝과 관련됨.
* Perception의 많은 알고리즘이 Deep learning 기반으로 변화하면서, 컴퓨팅 파워에 대한 수요가 급증
* 자율주행은 빠른 속도로 움직이는 환경이기 때문에 검출 성능 뿐만 아니라 검출 속도도 중요한 키워드
* Model Quantization, Pruning, HardWare Optimization 등 다양한 최적화 방법이 존재한다.

### Perception & Deep learning 기초
* 실제 Perception 프로젝트의 파이프라인 요소를 학습한다.
* Object Detection을 활용한 간단한 Perception 프로젝트를 수행한다.
* 원하는 객체 인식 모델 선택, 원하는 데이터 셋 선택, 원하는 결과가 나오도록 프로젝트 진행
* 딥러닝 기술이 실제 서비스 환경에 적용되기 위해서는 두 가지 문제를 해결해야함/
* 1. 인식해야하는 대상에 대한 데이터는 어떻게 준비하는가 - 데이터를 구축하는 방법을 익힌다. (어떤 객체를 검출, 데이터셋에 없을때는?)
* 2. 인식하는 환경 또는 대상이 변화하는 경우 어떻게 대응해야하는가 - 변화에 대응 가능한 방법을 마련한다. (정밀지도, 사람 검출)


* 유명한 데이터 셋을 참고하여 데이터는 어떤 구조로 저장되는지 학습
* 다양한 모델은 어떤 자료구조로 학습데이터를 입력하는지 학습 (json, yaml)
* 임의로 선택한 모델과 임의로 선택한 데이터를 가지고 모델 학습을 진행

* vision 기반의 Perception 프로젝트를 수행하기 위한 응용 방법을 학습한다.
* vision 기반으로 실제 객체의 위치를 추정하는 방법을 학습한다.

* Deep learning을 활용할 때, 발생하는 문제가 무엇인지 학습한다.
* 데이터의 중요성을 체감한다.

![image](https://user-images.githubusercontent.com/55529455/166206331-14c8fc91-595a-4254-9c40-ba04841caf20.png)

















