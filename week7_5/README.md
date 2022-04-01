# 강의 요약

> * 크기 불변 특징
> * Harris, GFTT, FAST 코너의 문제점
> * 이동, 회전 변환에 강인
> * 크기 변환에 취약

> * 호모그래피와 영상매칭
> * SIFT를 이용한 영상 매칭 : 영상 위치 판별

> * 코너점을 찾는 이유 = 각 코너마다의 정보를 이용하여 사진의 매칭을 수행 할 수 있기 때문에
> * 문제점 = 코너점이 어느정도의 크기변화는 괜찮음. 하지만, 너무 크기가 커지거나 작을 경우에는 에지로 추출할 수 있음.
> * 따라서 다양한 크기 관점에서 특징 검출이 필요함.
> * 특징점(지역) = 키포인트 = 관심점
> * 기술자 = 특징 백터
> * 이동, 회전, 크기로 변환 했을 때, 픽셀로만으로는 찾기 힘듬. 그래서 부분영상 히스토그램 같은 방법을 사용. = 256개의 실수값 = 특정 벡터
> * 4개의 실수 값으로 표현 할 수 있음 (0, 45, 90, 135도, 각도를 기준으로) = 4개의 bin (각 기준의 사이)
> * 이 방법을 에지 방향 히스토그램이라고 함.

> * 크기 불변 특징점 검출 방법
> * SIFT, KAZE, AKAZE, ORB 등 다양한 특징점 검출 방법에서 스케일 스페이스, 이미지 피라미드를 구성하여 크기 불변 특징점을 검출

> * SIFT = Scale Invariant Feature Transform
> * OpenCV에 들어가 있었음. 코드는 open, 하지만 상업적인 용도는 사용하면 안됨.
> * 알고리즘에 대한 특허는 2021년으로 종료됨.

> * SIFT 계산 단계
> * 검출, 기술 단계로 구성됨.
> * 1. 스케일 스페이스 = subsampling(resize) 할 때마다, 가우시안 블러를 하면서 줄여나감.
> * 이전 영상에서 가우시안 블러를 적용한 영상에 이전 영상을 빼게 되면 DOG (Differenece of Gaussian)이 출력되게 됨.
> * 2. 키포인트 찾기 = LOG 대신 DOG 영상의 모든 점에서 local maxima 또는 local minima를 선택
> * LOG = (laplasian of Gaussian) = DOG와 다르게 미분한 영상

![image](https://user-images.githubusercontent.com/55529455/161195968-83deba35-1ccf-40f2-ac64-6513d59f9a98.png)
> * 가우시안 함수를 2번 미분한것과 뺀것과 비슷하다.
> * 키포인트를 찾았으면, 서브픽셀 정확도를 올리고, 낮은 대비 극점 제거, 에지 성분 제거하면 그림이 나옴.

![image](https://user-images.githubusercontent.com/55529455/161196184-55c64dbe-ca35-43f8-9751-47497ef25aef.png)
> * 검출된 각 원은 보는 관점에서 달라짐. (resize 얼마나 했나)
> * 각 키포인트는 위치, 스케일, 기준방향 정보를 가짐 -> 이를 이용하여 크기, 방향에 불변한 특징 벡터를 추출. = 주된 방향 성분을 찾음.

> * 키포인트 기술자
> * 각 키포인트 위치에서 스케일과 기준 방향을 고려하여 사각형 영역을 선택
> * 사각형 영역을 4x4 구역으로 분할하고, 각 구역에서 8 방향의 방향 성분 히스토그램을 구함 = 4x4x8 = 128 차원의 벡터 (float)

![image](https://user-images.githubusercontent.com/55529455/161196542-ae34c684-193b-4550-8a07-1f6c52bf9ce4.png)

> * SURF (Speed Up Robust Features)
> * SIFT를 기반으로 속도를 향상시킨 크기 불변 특징점 검출 방법
> * DOG 함수를 단순한 이진 패턴으로 근사화
> * 적분 영상을 이용하여 속도 향상

> * KAZE
> * KAZE(바람) = 비선형 스케일 스페이스에서 공기의 흐름
> * 가우시안 함수 대신 비선형 확산 필터(nonlinear diffusion filter)를 이용하여 특징점을 검출
> * SURF 보단 느리지만, SIFT보다 빠르고 동등한 성능

> * BREIF
> * 이진 기술자를 이용한 빠른 키포인트 기술 방법 (not detector)
> * 키포인트 주변 픽셀 쌍을 미리 정하고, 픽셀 값의 크기를 비교하여 0 또는 1로 특징을 기술
> * 매칭 시 Hamming distance 사용 = XOR 논리 후, 0개 개수를 카운트.

![image](https://user-images.githubusercontent.com/55529455/161198874-eac397f6-d822-4635-8fd4-fa783874b7f9.png)
![image](https://user-images.githubusercontent.com/55529455/161199537-83d52230-d0fb-4dc4-a854-c6a1b0247737.png)
```
> * Ptr<Feature2D> detector = (사용하고자 하는 키포인트 기술)::create()
> * vetcotr<KeyPoint> keypoints
> * detector->detect(src, keypoints)
> * detector->compute(src, keypoints, dst)
> * detect + compute = detector->detectAndCompute(src, NoArry(), keypoints, dst)
> * 
```
> * 기술자
> * 각각의 특징점 근방의 부분 영상을 표현하는 실수 또는 이진 벡터
> * OpenCV에서는 Mat 객체로 표현함 = 행 개수 (특징점 개수), 열 개수 (특징점 기술자 알고리즘에 의해 정해짐)
> * 모든 특징점 벡터 값을 저장할 수 있는 2차원 백터로 나오게 됨.
> * SIFT는 128개의 열, KAZE는 64개의 열, SURF는 64개의 열로 구성됨.

![image](https://user-images.githubusercontent.com/55529455/161201062-c98bb345-d152-4a4c-b91e-14c24fda0424.png)

> * 이진 기술자
> * 이진 테스트를 이용하여 부분 영상의 특징을 기술함.

![image](https://user-images.githubusercontent.com/55529455/161201192-d92eb685-2780-4d47-bfe2-d34b7071a40e.png)
![image](https://user-images.githubusercontent.com/55529455/161201293-0d135383-4a46-4742-b05e-c31577783e9f.png)
![image](https://user-images.githubusercontent.com/55529455/161201937-12a930b8-961e-43b1-818d-00211fd9d901.png)

> * 특징점 매칭
> * 두 영상에서 추출한 특징점 기술자를 비교하여 유사한 기술자끼리 선택하는 작업.
> * 각 두 영상에서 나오는 특징점 백터를 계산하고, 보통 유클리디안 디스턴스를 이용하여 계산하게 됨.
> * 잘못 매칭 되는 경우가 많음. -> 데이터를 정제할 필요가 있다.






