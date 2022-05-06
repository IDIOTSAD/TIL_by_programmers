# 강의 요약

### Perception Application 2
* Computer Vision을 활용한 Autonomous Vehicle Perception을 공부한다면 논문 몇가지 추천함.
* Moblieye CEO 및 Computer Vision 전문가로 유명한 Amnon Shashua
* Google Scholar - https://scholoar.google.com/citations?user=dwi5wvYAAAAJ&hl=en&oi=ao

* 1992 - Geometry and Photometry in 3D Visual Recognition
* 2000 - Trajectory Triangulation : 3D Reconsutruction of Moving Points from a Monocular Image Sequence
* 2003 - Vision-based ACC with a Single Camera : Bounds on Range and Range Rate Accuracy - 중요

## Vision-based ACC with a Single Camera : Bounds on Range and Range Rate Accuracy
### Abstract
* 비전 베이스 ACC에 관한 내용. (Adaptive Cruise Control)
* 단안 카메라를 활용한 범위 (깊이 정보, 거리) 추정 방법에 대한 논문 - 지금도 쓰이고 있음.
### Introduction
* 직접범위(direct range) - RADAR, LiDAR, Stereo Image 등 범위 정보를 직접 제공하는 것
* 간접범위(indirect range) - 범위 정보를 추정하는 방법(=laws of perspective)을 사용하는 것.
* 논문에서는 간접 범위를 사용하여 상용 수준의 ACC를 만드는 것을 목표로 한다. - 단안 카메라 사용
* 사람의 시각 시스템(스테레오)의 베이스 라인은 사람의 손이 닿는 범위 및 더 먼거리에서 대략적으로 거리 측정하도록 설계됨.
* 반면 ACC 어플리케이션은 사람이 시각적으로 측정할 수 없는 100m에 도달하는 거리 측정을 필요로 함.
* 따라서 이러한 맥락에서 발생하는 질문은 거리 제어에 필요한 측정 정확도는 무엇일까?
* RADAR, LiDAR에 의해 제공되는 거리의 정확도는 거리 제어에 충분함.
* 그러나 사람의 시각 시스템을 보면 원근법칙(laws of perspective)만으로 만족스러운 성능을 나타낼 수 있음.
* 단안 시각 시스템에서의 도전 과제는 두 가지 있음.
* 1. 대상 분할에 대한 깊이 정보
* 2. 깊이 정보는 패턴 인식 기술에 크게 의존함. - 퍼셉트론, 신경망
* 이 논문의 핵심 질문은 타겟이 검출된 상황에서 원근 법칙과 망막 발산(retinal divergence)를 사용하여 ACC의 요구 정확도를 만족할 수 있을까?
### Range
* 원근법을 사용하는 방법은 두 가지 단서를 사용함.
* 1. 차량의 크기
* 2. 차량 바닥의 위치
* 도로면의 기하학 정보를 활용하면 더 나은 결과를 얻을 수 있음.
* 평평한 바닥과 광학 축이 노면과 평행하도록 설치된 카메라가 있다고 가정 할 때, 카메라로부터 Z 만큼 떨어진 노면은 이미지에서 높이 y를 투영함.
* y = fH / Z, H는 카메라의 높이

![image](https://user-images.githubusercontent.com/55529455/167088325-913e801c-adeb-4c60-9d40-1a0efa65b3cb.png)
![image](https://user-images.githubusercontent.com/55529455/167088510-c4542d7c-97fe-42d9-a02e-74484eaae809.png)
![image](https://user-images.githubusercontent.com/55529455/167088732-1b5f84eb-d64b-4240-bd4c-dc0cfbe8159d.png)
* 하지만, 다음과 같은 상황에서는 오차가 발생 할 수 있음.
* 1. 카메라의 광학축이 노면과 평행 할 수 없다. - 수평선이 이미지 중앙에 위치할 수 없다. - 카메라와 노면이 평행하지 않음.
* 2. 카메라의 장착각도와 차량의 움직임(pitch)에 의해 변화가 생길 수 있다. - 차량의 급가속, 급정거 순간
* 3. 이러한 오차를 보정하더라도, 차량이 노면과 닿는 지점의 이미지 좌표를 결정하는데 있다. (현실세계에서 거리 정보는 실수, 이미지 좌표는 정수)

![image](https://user-images.githubusercontent.com/55529455/167089419-250f4be9-7aa6-49c2-921d-919552aa9368.png)
![image](https://user-images.githubusercontent.com/55529455/167090600-44901a1e-05bc-46bd-a4e9-1452a4ec07a5.png)
* n은 오차를 의미함.

* 거리(depth) 오차는 2차적으로 증가하고, (먼 거리 일수록 오차가 급격히 커짐)
* 타겟까지의 거리가 증가함에 따라 거리의 백분율 오차가 선형적으로 증가한다.
* 640 x 480 이미지에서 FOV 47도, f = 740 pixel 이라 하고, H는 1.2m, 1픽셀에러, 거리 오차 5%가 있을 때, Z의 값은?
* Z = (Z(err) / Z) * f * H = 0.05 * 740 * 1.2 = 44m가 나옴.
* Z^2 = (Z(err) * fH) 로부터 시작된다.
* Z(err) = nZ^2 / (f * H + nZ) 이지만, n은 1이기 때문에 사라짐. fH의 값이 매우크고, Z의 값이 매우 작기 때문에 Z를 무시한다.
* 따라서 Z^2 / fH가 된다. => (Z(err) / Z) = Z / fH가 되므로(거리 오차), 0.05가 되는 것.
* 약 5%의 에러를 가지는 지점이 45m이기 때문에, 90m에서는 10%의 오차를 가진다. ACC를 설계하는 관점에서는 괜찮은 오차임.
* ACC에서는 거리의 비율이나 상대속도가 중요함. 앞 차량의 거리가 45m 인지 42m인지는 중요하지 않음.

### Range Rate
* 레이더 시스템에서는 도플러 효과를 사용하여 범위 속도 및 상대 속도를 측정함.
* 비전 시스템에서는 이산 차분에서 다음과 같이 계산됨.
* v = (delta)Z / (delta)t - Z는 앞차와 나의 거리, t는 앞차와 나의 시간 차이 (속도 = 거리 / 시간 이용)
* 두 개의 서로 다른 지점에서 Z에 대한 에러를 제거하면 정확한 측정 값을 얻을 수 있다. (단순 이산 시간 차이만을 가지고 계산하면 부정확)
* 섹션 3.1에서 스케일 변경에 대한 계산 방법을 설명하고, 섹션 3.2에서 정확한 이산 시간 차이를 계산하는 방법을 소개한다.

![image](https://user-images.githubusercontent.com/55529455/167100868-b75cc033-4b04-428a-bd31-77c41c00d2ec.png)
![image](https://user-images.githubusercontent.com/55529455/167101335-c76caf57-3463-41d4-b0e9-fa2e6ce0889c.png)
![image](https://user-images.githubusercontent.com/55529455/167106169-c9da9f75-805e-4d0b-9795-55e44536c2d0.png)
![image](https://user-images.githubusercontent.com/55529455/167106244-840ee5dd-7b59-4396-83b7-e91299aa8457.png)
![image](https://user-images.githubusercontent.com/55529455/167106286-551fd144-4b7f-4950-8ba6-e64370fcdd25.png)
![image](https://user-images.githubusercontent.com/55529455/167106344-060d1a00-c0e1-4a23-a7e1-dbf9905b0921.png)
![image](https://user-images.githubusercontent.com/55529455/167106403-976affd6-f0cb-471f-8b4d-686802e839fc.png)

### Extrinsic Calibration
* 1. Computer Vision에서는 사용하는 좌표계는 월드, 카메라, 이미지, 정규이미지 좌표계를 사용
* 2. 카메라는 3차원 공간에 존재하는 물체를 2차원 공간에 투영하는 센서
* Extrinsic Calibration은 월드 좌표계 -> 카메라 좌표계, 카메라 좌표계 -> 월드 좌표계를 이해하기 위한 과정이다
* 실제로 존재하는 3차원 공간에 대한 정보를 다룸.
* Compuver Vision을 활용한 자율주행 분야에서 Extrinsic Calibration은 두 가지 활용 방법을 위해 Extrinsic Calibration을 수행
* 1. Sensor Fusion을 위한 정보로 활용
* 2. Perception Application을 위한 정보로 활용
* Extrinsic Calibration은 환경과 조건에 따라 목적과 방법이 달라짐.
* 다양한 방법론을 소개하고, 자신에게 주어진 환경에 맞는 고유한 방법을 찾아야함. (범용적인 솔루션 없음. - 센서의 종류, 개수, 장착위치 등의 변수)

* 자율주행 차량은 자동차의 경우, 모든 정보를 자동차 좌표계에 정보를 통일한다.
* 일반적으로 자동차 좌표계는 후륜 구동축의 중심 지면을 원점으로 한다.
* 자율주행 차량에 장착되는 센서는 그 종류가 다양함.
* 1. 카메라 : 카메라 좌표계를 따름.
* 2. LiDAR : LiDAR 좌표계를 따름.
* 3. GPS, IMU : 각 센서의 좌표계를 따름.
* 각 센서의 장착 위치가 다르고, 사용하는 좌표계가 다르기 때문에 이를 통합하는 과정이 필요하다 (Sensor Fusion)
* 따라서 카메라의 장착 위치와 자세를 파악해야한다. - 차량 좌표계에서 카메라 좌표계로 가면 Ext, 반대로 하면 Ext 역수

![image](https://user-images.githubusercontent.com/55529455/167109309-b1bf758f-adab-469d-940b-9a706a841405.png)
* rvec, tvec 값을 이용하여 objectPoint를 투영하면 해당 평면의 3차원 물체가 투영됨.
* 그러나, 카메라가 존재하는 공간은 3차원이기 때문에, Extrinsic Calibration의 origin을 보드로 설정하기 어렵다.
* objPoint의 origin을 어느 한 점으로 설정하고, 카메라 캘리브레이션을 수행하면 해당 origin에 대한 rvec, tvec을 얻을 수 있음.
* 아래 사진에서 Tire Clamps와 Distance meter을 이용하면, 후륜 축으로부터의 거리를 파악 할 수 있다.
* 두 개의 거리 측정기를 사용하여 Calibration Pattern과 차량의 수평을 조정 할 수 있음.

![image](https://user-images.githubusercontent.com/55529455/167110879-6e52cf41-971f-4320-a9d5-23ab379b9fbd.png)
![image](https://user-images.githubusercontent.com/55529455/167111438-bdb8e2fe-adcb-44fe-a9c5-048a93cd8f6f.png)
![image](https://user-images.githubusercontent.com/55529455/167111516-7a630e56-a0bf-4c08-99be-69dd75eb58fc.png)

* Mobileye와 같이 높이와 거리를 통해서도 응용이 가능함.
* 다수의 Calibration Pattern을 사용하는 방법도 존재함.
* Calibration Pattern 사이의 rvec, tvec을 계산하면(reconstruction), 카메라에서 촬영한 다수의 Pattern들의 imagepoints로 카메라의 자세를 파악할 수 있다.
* 대표적인 Extrinsic Calibration - Camera-LiDAR Calibration

![image](https://user-images.githubusercontent.com/55529455/167113947-c7536e7f-9a51-4d75-81c8-912894aefd56.png)
![image](https://user-images.githubusercontent.com/55529455/167113988-31e2b73f-1ca2-4e86-a047-58c65cd3ca68.png)

* 이렇게 얻어낸 objpoints와 imgpoint로 PnP 문제를 풀면, LiDAR -> Camera의 rvec, tvec을 계산 할 수 있음.
* LiDAR 데이터와 함께 Projection 하면 Image 위에 LiDAR 데이터를 올릴 수 있음.
* 단, 여기서 얻어낸 rvec, tvec으로 이미지 데이터로 3차원 공간 정보를 복원할 수 없음. (무수히 많은 해가 존재)

![image](https://user-images.githubusercontent.com/55529455/167114362-66a18416-0151-4986-a59f-19b25d46e478.png)
* x가 음수인 경우에는 사용 안하도록 필터링을 수행 해야함.

![image](https://user-images.githubusercontent.com/55529455/167114479-009281b5-1a6b-497f-aba4-6bfbb3bbaadc.png)


















