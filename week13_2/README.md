# 강의 요약
## General Triangulation
* 이전에 배웠던 E-matrix, F-matrix는 위치추정쪽에 가깝다.
* Triangulation - 매핑의 가장 첫 단계, 두 개 이미지 사이에서 회전값을 알고 있고, 피쳐들간 Corresponding 알고 있을 때,  3D의 x, y, z의 coordinate 값을 복원
* 2D -> 3D 공간으로 매핑이 가능해지게 됨.
* 피쳐간 ray를 그리게 되면, n개의 3D 포인트 xn에서 만나게 됨. - 거리값도 추정가능.
---
* 3D 에서는 완벽하게 약간의 간격을 두고 떨어져 있음.
* 어떻게 해야하는가? - 두 ray가 만날 수 있는 가장 가까운 점의 평균 위치 H값을 찾음.
* 같은 정도의 노이즈가 있다는 전제 하에, ray를 조금씩 이동시켜서 중간점 h를 찾는 것이다.
* s, r = 다이렉션 벡터이고 람다, 뮤는 거리값을 의미함.
* 여기서 p와 q는 알고 있는 값, 람다, 뮤는 알고싶은 값, r, s는 다이렉션 벡터
* kx' - 캘리브레이션 된 카메라에서 왼쪽 카메라의 피쳐 위치, kx'' - 캘리브레이션 카메라에서 오른쪽 카메라의 피쳐 위치
* kx' = (x', y', c)^T를 의미함 - x', y'는 이미지 픽셀 좌표, c = focal length (camera construct)
* R'^T = Rotation 값의 전치행렬, SO 매트릭스에서 전치는 역행렬임. (world to camera의 역행렬은? - 전치행렬을 곱하기 때문에 카메라 좌표계에서 월드 좌표계로 감.)
* 따라서 3D ray가 형성 될 것이다.
* 하지만, 2개의 수식으로 바로 intersection을 구할 수 없음
* 두개의 3D ray는 instersection하지 않기 때문에(실제로)
* 두 점이 가장 가깝게 거리를 가지는 지점 부분인 선분FG가 ray Q와 P에 대해서 수직이어야 한다.
* 수직인 두개의 라인끼리 dot 하면 0이 된다.
* 람다와 뮤를 구하면 F, G를 구할 수 있고, H의 값은 (F + G) / 2 - 실제 알고리즘에서는 F G의 비중을 다르게 해서 (weight) 조정하게 됨.

![image](https://user-images.githubusercontent.com/55529455/171091795-9c726f5c-4dc6-4861-9bad-f9afdf88d382.png)
![image](https://user-images.githubusercontent.com/55529455/171106578-15cf78ff-fb30-4dd9-bb5a-e3db3eae8585.png)
![image](https://user-images.githubusercontent.com/55529455/171109168-edd6ec6b-663b-447b-b0de-b58f5d260efb.png)

## Stereo Triangulation
* 둘 간의 baseline, 상 x', x''가 맺히는 상 위치를 알고 있다.
* 피쳐의 위치의 차를 알고 있다 (Parallax, Disparity)
* 비례식을 이용하여 문제를 푼다. O''와 P'' 사이의 거리(C)와 x''의 크기, X에서 오른쪽 끝 대칭점까지의 거리를 알고있는 것을 이용함.
* Y는 이러한 식을 이용하기 어려움 - 보통의 3d ray는 서로 intersection하지 않는 경우가 많음. 
* y값이 맞으면 x가 맞지 않을 경우가 많다.
* 왼쪽 y'과 오른쪽 y''를 구한 후, 평균 값을 구해주면 된다.

![image](https://user-images.githubusercontent.com/55529455/171109546-4f835ad0-1ab4-4fdd-b2d9-2840bede6901.png)
![image](https://user-images.githubusercontent.com/55529455/171113829-debecf1d-760e-49f0-85e9-4fcd266f2efc.png)
![image](https://user-images.githubusercontent.com/55529455/171114390-baf38ee3-4262-49ac-939b-896a6b01fe75.png)
![image](https://user-images.githubusercontent.com/55529455/171114908-7fb485cc-5887-4340-a003-4c743ff23f20.png)

## Persepective-n-Points
* PnP problem - Persepective-n-Points의 약자, n은 n개 할 때 n임.
* 2D와 3D간의 correspondences가 주어졌을 때, 월드 - 카메라를 추론하는 것이 목적임.
* 카메라가 3D 맵을 보고 있을 때, 이미지 피쳐와 3D 포인트 간의 correspondences가 주어졌다면, 이 정보로 카메라 Pose를 추정하는 것이 목표
* 몇개를 쓰냐에 따라서 n의 개수가 정해짐. 
* 왜 중요할까? - 이미지에서 피쳐를 뽑고 매칭함으로써 맵에서 부터 나의 위치를 찾아주는 중요한 기술. - SLAM..?
* 실제로 localization 할때, PnP 기법이 가장 중요함.
* 3d x 점이 담고있는 디스크립터들과 현재 뷰에서 보이는 디스크립터와 매칭하여 2D 2 3D 코디네이터를 구현.
* P3P가 minimum solver가 됨.
* 노이즈를 고려하지 않은 순수한 계산 방법

![image](https://user-images.githubusercontent.com/55529455/171126548-74f3d110-7cd3-4658-bb1c-251cd41c56b9.png)

## Minimal solver - P3P Grunert method
* P3P를 풀기위한 기본적인 전제조건
* x1, x2, x3 위치를 알고 있는 상황에서 x'1, x'2, x'3 를 알고있는 상황
* ray 들마다의 각도를 계산 가능하지만, x0에서 x1,x2,x3의 길이는 모름.
* 두 가지 내용을 추론하게 됨.
* 1. x0와 xn의 길이를 추론
* 2. 길이와 각도를 기반으로 회전행렬 추론

![image](https://user-images.githubusercontent.com/55529455/171127139-307dce01-ede9-46c2-b7aa-264705476e19.png)

---
![image](https://user-images.githubusercontent.com/55529455/171129492-1dc47417-99de-43c3-b498-bf3204f8db7c.png)
* xi = ray들, x0 = camera center kxis는 object를 향하고 있는 ray의 방향 벡터, si = 스케일, R은 world 계에서의 회전값
* R은 world to camera기 때문에 camera 좌표계에서 표현된다는 것을 의미
* kxis를 좀 더 자세히 보면, sin(c)에서 c는 camera constant, focal length를 의미함. 여기서 focal length는 plane에서 이미지 센서 방향이므로 -를 붙임.
* N은 정면으로 가는 벡터를 노멀라이제이션을 해주는 펙터 (유니벡터), 방향을 나타내주는 xi (픽셀단위이므로 K(캘리브레이션)의 역행렬 곱해줘야함)
---
* Step 1 - s1, s2, s3를 얻고 싶다!

![image](https://user-images.githubusercontent.com/55529455/171131752-72ab9a5c-f9fe-47bf-9d00-9558bddca7df.png)
![image](https://user-images.githubusercontent.com/55529455/171131880-024258fa-7973-4293-a852-21d7e1e05241.png)
![image](https://user-images.githubusercontent.com/55529455/171133074-fa8ea312-0ee5-400d-a4c7-585a3f623c84.png)
![image](https://user-images.githubusercontent.com/55529455/171133744-ddc41586-9607-4f81-922b-dc6745d671a5.png)
![image](https://user-images.githubusercontent.com/55529455/171133952-680c44f4-62f9-4d3f-befb-3799834fda78.png)

* 각 점의 각도를 구함. (알파, 베타 ..)
* 3D 포인트간의 거리 (a, b, c)를 구하고, 이를 cos 공식을 이용하여 s1, s2, s3를 계산함.
* 그리고, u를 중심으로 보게 되면 u를 제거 하고 식을 재정립한다. 4차 방정식이 나옴 
* 4차 방정식으로 풀게 된다면, 4개의 답이 나오게 되는데, 1개를 제외한 나머지는 기하학적인 값.
* 1. 다른 센서를 사용해서 회전 값을 찾아서 값을 검증하는 방법 - 카메라만 사용하는 V-SLAM에서는 사용 불가
* 2. 다른 포인트 값를 가져와서 다시 회전 값을 찾아서 검증함. 카메라 위치를 잘 찾지만, 1개의 데이터가 추가됨.
* P4P가 아니냐! - 의견도 있음



