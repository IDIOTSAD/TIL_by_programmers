# 강의 요약

## 3D회전과 이동

### Rigid Body
* 위치에 대한 정보를 x, y, z 값으로 표현 가능
* 단순히 위치 값이 아닌, 방향도 있음.
* ex) 카메라 - 카메라가 어떤 방향을 보는지도 알 수 있음.
* Position (위치) + Orientation (방향) = Pose
* 카메라좌표계의 tx, ty, tz 를 월드 좌표계에서 본다면? - 좌표 변환이 필요함.
* 좌표 변환에 필요한 점 - 2개 좌표에 대한 Orientation 좌표와 Position 좌표가 필요함.
* Orientation - 회전값, Position - 평행이동값
* Ridge body motion - 3D -> 3D transform (유클리디안 변환, 유클리디안 월드 - 또다른 유클리디안 월드)
* 유클리드 기하학에 맞춘 법칙 - 유클리드가 붙음.
* 유클리드 공간에서 좌표계 표기법 - Cartesian Coordinate, 우리가 살고있는 공간은 유클리드 공간.

## 다양한 회전 표현법
### Euler Angle
* Roll / Pitch / Yaw
* 각각의 축을 의미, 3D rotation을 표현하기 위해 차례로 변환을 해줘야함.
* 장점 - 이해하기 쉬움
* 단점 - 최적화 하기 어려움 (미분이 가능해야 최적화 가능), 짐벌락 (Gimbal lock)
* 짐벌락 : 특정한 축의 위치에서 한 좌표가 회전할때, 3D 좌표가 2D 좌표처럼 표현되는 것을 의미 (하나의 회전 각도가 사라짐)

![image](https://user-images.githubusercontent.com/55529455/170526592-c35e6301-3689-488f-b28c-779df9bbc013.png)

### Axis-angle
* 물리학에서 벡터를 바라보는 방향으로 보는 것.
* 방향과 크기를 가지는 것이 벡터임.
* 회전에 하는 축에 방향과 얼마나 회전을 하는지 각도 2개를 따져서 물리학에서의 시점으로 봄.
* 축 + 각 = 축각도 = 로테이션 벡터 = 로드리게스 공식
* 메모리의 효율이 다른 회전 표현법보다 좋음. (3개의 파라메터로 각도 표현 가능함)
* 4개의 파라메터는 9개보다 2배 이상 좋고, 3개만 쓰면 메모리 효율이 3배 좋아짐.

![image](https://user-images.githubusercontent.com/55529455/170558030-ea171b27-c90f-4f66-9319-ea497173f9ee.png)

### Quaternion
* 회전을 표현하기 위한 알맞은 회전축의 개수? - 3개면 안되나? : 이 방식은 싱귤래리티 문제 발생
* 위 문제를 발생하지 않는 최소한의 파라메터는 4차원으로 표현하면 됨.
* 쿼너티엄은 4개의 파라메터를 사용하는 것.
* No singuarity로 인해 미분이 가능해짐 - 최적화가 가능해짐. SLAM에 사용하기 좋음. - 단, 4차원에 대한 이해가 필요함.

### SO(3) Rotation Matrix
* Special Orthogonal Matrix (3D) - SO(3)
* 3개의 파라메터로 구성됨. 회전만 표현해주는 매트릭스.
* 1. x,y,z가 회전을 해도 기존의 x,y,z축이 모두 회전 후에도 수직을 유지해야함.
* 2. x,y,z축이 벡터의 길이가 바뀌면 안됨.
* 즉, 행렬식이 1이 나와야 한다는 점이다. ((a b) (c d))가 있다면, ad - bc
* 역함수(A^-1)는 매트릭스(A)에 트랜스포즈(A^T)를 한 값이랑 같다.
* Rx 순으로 Rz까지 곱한다.
* 여러개의 회전을 중첩해서 하나의 회전을 표현하는데 좋은 방법
* 하지만, 3축의 회전을 표현하기 위해서 9개의 파라메터를 사용해야함. - 메모리를 많이 차지함. 
* 여러개의 매트릭스를 1개의 매트릭스로 통합 할 수 있다는 점이 있다. - 메모리를 어느정도 절약 가능함.
* 조건들이 상당히 있음. - 최적화를 하기 위해서 바로 사용하는 것은 어렵다.
* 미분은 가능함. - 자코비안 매트릭스를 얻을 수 있지만, 반복하게 된다면, 반복 결과가 SO(3) 결과가 나올지는 모름. (반복 = 이터레이션)

![image](https://user-images.githubusercontent.com/55529455/170562244-6a4cbeba-701f-42af-a90f-9b1d4e422a1c.png)

### Translation
* {x, y, z}로 표현함
* 벡터로 표현해주면 됨. - mm, cm, m 단위만 잘 조절해주면 됨.

### Transformation
* SE(3) 매트릭스 - SO(3) 매트릭스 + Translation (4x4)
* Special Euclidean Group (3D) \[ (R(3x3), t(3x1)), (0, 1) ]

![image](https://user-images.githubusercontent.com/55529455/170563975-42742139-a39b-4e61-aa36-8c070c80fcf7.png)

## Projective geometry - 사영기하학
### 3D World vs Photo
* 닮음을 이용한 Similarity Geometry, 한점만 이동 시키는 경우에 가능한 Affine Geometry가 있음.
* 사영기하학도 하나의 기하학임.
* 사진 속 차선을 생각했을 때, 유클리디안 기하학에서 평행함 (무한의 거리에서 두 선이 교차함 - 유클리디안에서는 무한은 숫자 표현 안됨.)
* 유클리디안 에서 표현하던 무한의 거리를 픽셀에서는 표현할 수 있는 영역이 점점 작아지면서 교차하게 된다.
* 미술학에서는 소실점이라고 함.

### 원근법
* 실제 세계에서는 평행이었던 것이 사진에서는 평행하지 않는가? - 원근법 (가까이 있는건 크게 보이고, 멀리 있는건 작게 보임)
* 우리는 물체의 실제 크기를 알 수 없음. 3D의 데이터를 2D 이미지로 투영하면서 depth 이미지가 소실됨.
* 유클리디안 트랜스폼이 되기 위해서는 orthogonality 유지, 평행 유지, 여러가지가 있음.
* 프로젝티브 트랜스폼은 직선인 물체가 직선으로만 나오면 된다.

### Vanishing point (소실점)
* 유클리디안에서는 평행한 직선은 무한에서 교차하는데 무한은 관측 불가능함.
* 무한의 거리를 소실점에서 관측 할 수 있게 됨.
* 3D에서의 무한은 2D에서는 유한으로 매핑이 가능해지는 것이다. - 수학적으로 표현이 가능해진다.
* 3D에서 2D를 매핑할 때 필요한 모든 위치를 수로 표현할 수 있고, 무한의 교차점을 표현 할 수 있는 것 - 2가지가 새로운 기하학의 특징이 됨 (사영기하학)

### Hierarchies of geometries
* 유클리디안, 시밀러티, 어파인, 프로젝티브
* Euclidean - Rotation + Translation 표현 가능
* Similarity - Euclidean + uniform scaling 표현가능, length 정보 소실
* Affine - Similarity + Non-uniform scaling + shear 표현 가능, Angle / length-ratio 정보 소실
* Projective - Affine + projection 표현 가능, incidence , cross-ratio 정보 소실
* Projective geometry - N+1 차원 > N 차원 투영 (차원을 낮출 때 사용하는 기하학)
* {x, y, z} + {scale} = Homogeneous coordinatiates

## Homogeneous coordinates
### Definition (Plucker definition)
* Homogeneous coordinates 정의
* x라는 개체에 Homogeneous coordinates 0이 아닌 어떤 스칼라 값을 곱해도 coordinate는 같은 값을 의미함.
* x = lambda * x 라고 표현 할 수 있음.

![image](https://user-images.githubusercontent.com/55529455/170579728-b5a71336-b8c9-4632-87e1-3c4aa2aca5d4.png)
![image](https://user-images.githubusercontent.com/55529455/170579880-2e1611a7-2b79-4dcf-9fcb-a182377b21ad.png)

* 기존의 차원과는 다른 scale의 차원이 생김.
* x = {x, y} 일 때, x = {x, y, 1}로 표현이 됨. - scale의 값이 1임
* 어떠한 스칼라가 곱해져도 결국은 scale 값으로 나눠주면, {x, y, 1}로 돌아옴.
* {x, y} = Cartesian coordinates, {x, y, 1} = Homogeneous coordinates

### Projective space
* u, v 는 x, y축 (2D Plane의 좌표계)
* w 축? - 호모지니어스 좌표계의 scale을 의미함.
* 색칠되어있는 plane = 유클리디안 공간 - Projective 속에 있는 하위 공간을 의미함.
* x 점 좌표는 어떻게 표현이 될까? (0,0,0) ~ (x, y, 1)을 지나서 lambda(x, y, lambda)로 표현이 될 수 있다.

### Euclidean space vs Projective space
* 유클리디안 공간 - Cartesian coordinates, (사영공간의 일부, scale 값이 1), 호모지니어스로 변환시 scale 값을 1을 추가하면 됨. (x,y,1)
* 사영 공간 - Homogeneous coordinates, 카티션으로 변경시, scale을 1로 만들고 scale 부분 벡터를 떼면 됨.
* 매트릭스를 호모지니어스로 변환이 가능한가? - 가능함. 3x3의 매트릭스를 4x4로 만들고, 마지막 부분에 0, 0, 0, scale 을 추가해주면 된다.

![image](https://user-images.githubusercontent.com/55529455/170582740-3c590b53-0865-4a2d-aa31-ec56a555659c.png)

## 핀홀카메라 투영
### Camera obscura
* 바늘구멍 사진기 (pinhole camera) - 정확한 2D 이미지를 구할 수 있었음
* 3D 세상과 비교하면서, mapping 수식을 발전 할 수 있었음.
* 두가지 물리법칙
* 1. 빛은 직선으로 이동한다. 이미지에 맺힌 상이 거꾸로 맺힌다는 것도 직선으로 빛이 이동한다는 것
* 2. 상맺힘 - 3D 이미지가 2D 이미지로 하나의 상으로서 투영됨.

### Morden camera - 핀홀 카메라와 원리는 같다.
* 렌즈를 통해 빛을 모으고 초점을 맞추기 위해 sw/hw 수정을 함.
* 하드웨어 수정 - 구멍의 크기를 바꾸거나, Exposure를 통해 전체 광량을 수정
* 소프트웨어 수정 - ISO gain, normalization을 통해서..

### Camera Projection
* 3D -> 2D 투영을 수학적으로 설명
* x = PX (X는 3D 코디네이터 포인트, P는 프로젝션 매트릭스, x는 2D 코디네이터 포인트)
* world coordinate system (3D) -> camera coordinate system (3D) -> image coordinate system (2D)
* 월드가 바라보는 위치를 카메라로 바라보겠다는 것 + 차원 축소

### world coordinate system (3D) -> camera coordinate system (3D)
![image](https://user-images.githubusercontent.com/55529455/170584065-6560e67a-4d03-4906-a366-368172c79d34.png)
![image](https://user-images.githubusercontent.com/55529455/170589909-6df2cf15-1438-46d7-b5e4-cf6c9cb9c31d.png)
* world frame은 사전에 우리가 정한 좌표를 의미함.
* camera frame은 카메라의 이미지 센서의 중심에 있음.
* world frame - camera frame 이동하면서, Xw가 Xc로 변환이 됨.
* 물체위치를 표시하는 방식을 물체와 카메라와의 상대적인 Pose로 하겠다는 것을 의미함. - world와 관련된 것을 모두 제거
* Xc가 가상의 이미지를 투과하는 것을 볼 수 있다.

![image](https://user-images.githubusercontent.com/55529455/170590365-bfe50d82-928b-4f46-b57f-1ce02122c0b1.png)
* z축은 카메라의 전방을 의미
* Image plane의 영점을 P라고 함 - 주점이라고 함.
* x_c를 보면, 가상의 image plane을 통과하는 것을 볼 수 있음 - x_im
* 이상한점? - 상이 똑바로 맺혀있다? 반대로 뒤집혀 있다고 배웠는데..
* focal point를 지나서 뒤집혀있는 것이 맞음. 하지만, focal point 앞으로 투영된 이미지를 사용하는 것이 관용
* focal point 앞으로 나둔 이미지는 뒤에 뒤집힌 상을 180도 회전 시킨 것과 같은 결과다.
* 수식에서 결과가 다르게 나오지 않음.

![image](https://user-images.githubusercontent.com/55529455/170590766-410b3d91-8fee-4d25-829e-39d62de7ff48.png)
* fx, fy = focal length (focal point와 가상의 image plane 사이의 거리)
* (x, y, z)를 (fx\*x/z, fy\*y/z)로 표현 할 수 있게 되었다. 하지만, C의 기준으로 되어있고, 이미지의 중앙으로 되어있음.
* 픽셀로 이미지를 표현할 때는 0,0은 이미지 좌측상단을 의미한다.

![image](https://user-images.githubusercontent.com/55529455/170591134-53f43704-199f-41d3-b5fe-f34efb97dfc0.png)
* 따라서 이미지의 중앙을 왼쪽 상단으로 옮겨주어야한다.
* width / 2, height / 2 의 값을 가져온다. 하지만, 실제 값으로는 어느정도 에러가 있다.

![image](https://user-images.githubusercontent.com/55529455/170591230-1e4e4649-0367-4421-bdda-da905cd33379.png)
![image](https://user-images.githubusercontent.com/55529455/170591388-61b21a10-908b-4fe0-b62a-c346b9f806ca.png)
![image](https://user-images.githubusercontent.com/55529455/170591429-9eb0476e-1654-4251-b187-4e398b58cd84.png)

## 카메라 센서의 구조
### Camera
* 카메라는 사진을 찍을 수 있고, 기록을 남기는 것을 의미한다.
* 하지만, 컴퓨터 비전에서는 










