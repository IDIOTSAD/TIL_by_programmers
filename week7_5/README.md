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
> * 이진 특징 벡터 계산 = 호밍 디스턴스 사용
> * 실수 특징 벡터 계산 = L2 노름 사용
> * 잘못 매칭 되는 경우가 많음. -> 데이터를 정제할 필요가 있다.

![image](https://user-images.githubusercontent.com/55529455/161204366-0eadbeb2-a680-4afc-bd40-9a3b4e19143b.png)
> * BFMatcher에서 BF = 브루트 포스 => 전역조사(무식하게 다 해본다)
> * Flann = Fast Library for Approximate Nearset Neighber (K-d Tree 사용)
> * 엄청 큰 데이터가 아닌 이상, BF로 해도 무방하다. (2D에서는)
> * 매칭 결과는 Dmatch 클래스로 반환됨. = 1번에서 나온 특징점 벡터가 2번에서 나온 특징점 어디로 연결되는지에 대한 정보
> * Dmatch 클래스에서의 distance 는 두 특징점 사이의 거리(비유사도)를 표현.

> * 좋은 매칭 선별 방법 1
> * 가장 좋은 매칭 결과에서 distance 값이 작은 N개를 사용
> * DMatch::distance 값을 기준으로 정렬 후, 상위 N개 선택
> * DMatch 클래스에 크기 비교 연산자 < 오버로딩이 distance 멤버 변수를 이미 사용하도록 되어있음

> * 좋은 매칭 선별 방법 2
> * knnMatch() 함수를 사용해서 두 개의 매칭 결과 반환
> * 가장 좋은 매칭 결과의 distance 값과 두번째로 좋은 매칭 결과의 distance 값의 비율을 계산
> * 이 비율이 임계값보다 작으면 선택함.

![image](https://user-images.githubusercontent.com/55529455/161205759-db888fa7-190d-48b5-a59a-9dccf7623cdc.png)

> * 호모그래피
> * 두 평면 사이의 투시 변환
> * 8DOF 최소 4개의 대응점 좌표가 필요

![image](https://user-images.githubusercontent.com/55529455/161206442-666863b3-3e89-4466-b24b-69823197c960.png)
> * 어떤 건물의 측면에서 봤을때와 정면에서 봤을 때가 다름.
> * 내가 정면에서 본 것 처럼 바꾸고 싶을 때 사용함.

![image](https://user-images.githubusercontent.com/55529455/161207059-976ef0c0-abcd-42c7-819c-764fc401b56d.png)

> * RANSAC
> * Random sample consensus
> * 이상치가 많은 원본 데이터로부터 모델 파라미터를 예측하는 방법 (이상치 = 거짓 데이터)

![image](https://user-images.githubusercontent.com/55529455/161207566-c6559732-cb41-4e0c-b053-f37bbe8110ee.png)
> * 완전히 잘못된 outlier가 있으면 데이터가 잘못 나옴.
> * 이를 제거함으로서 정확한 선을 표현하도록 함.
> * 임의의 두 점을 찾아 직선을 그림.
> * 나머지 점들과 직선 사이의 수직 거리를 계산하고, 에러가 허용 오차 안에 있는 점들의 개수를 구한다.
> * 랜덤하게 2개의 점을 계속 구해서 수십번 작업을 함.
> * 결국, 가장 많은 허용 오차 안에 있는 점을 가지는 두개의 점이 선택되게 됨.



