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




## Minimal solver - P3P Grunert method






