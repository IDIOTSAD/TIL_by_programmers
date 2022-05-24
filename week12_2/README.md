# 강의 요약

## SLAM 공부를 시작하면서
* Mathematics - Linear algebra, Probability & Statistics
* Computer Vision - Imaging, Image Processing
* Optimization - Optimization theory, Numerical optimization

### * 선형대수학 강의 추천
* youtube(이상엽) - 선형대수학
* gilbert strang - introduction to linear algebra 5th ed
* deisenroth et al - mathematics for machine learning part 1

### * 통계 강의 추천
* Evans and Rosenthal - Probability and Statistics

### * Image processing 강의 추천
* 황선규 박사님 - OpenCV 4로 배우는 컴퓨터 비전과 머신 러닝
* Opencv 공식 도큐먼트

### * Imaging & photography
* Marc Levoy - lectures on digital photography (youtube)

### * Optimization theory, Numerical optimization
* wright et al - Numeriacal optimazation ch8, ch10
* press et al - numerical recipes

### * SLAM
* youtube - cyrill stachniss lectures
* gao - introduction to visual slam
* ma - an invitation to 3-d vision

### * 이론 공부 - 공부방향
* github - 'changh95/visual-slam-roadmap'
* 카카오톡 오픈채팅방 - 저희는 SLAM 마스터가 될겁니다
* facebook group - SLAM KR

### * C++
* Marc Gregory - 전문가를 위한 C++
* Jason Turner - C++ baset Practices
* youtube - back to basic 시리즈

### * 알고리즘 / 자료구조
* https://www.cv-learn.com/20210214-data-structures-and-algorithms/
* 코딩테스트를 위한 자료구조와 알고리즘 with c++
* youtube - 이것이 취업을 위한 코딩테스트다 with python - C++도 나옴.

### * 소프트웨어
* 모던 C++ 디자인 패턴
* Robert C. Martin - 클린코더, 클린코드

## 확률과 통계 Primer
### State Estimation (상태 추정)
* 실제 세상에서 로봇이 자기자신의 위치를 정확히 추론? - 실제세상에서는 자기자신의 위치를 정확히 추론 불가능
* 센서정보를 통해서 얻어낸 후, 자기자신의 위치를 추론을 해야하는데, 노이즈가 있고, 센서는 확률분포적인 값을 하기 때문이다.
* 불확실성이 항상 내재되어 있음.
* 수식에 녹여내기 위한 방법으로 확률적으로 표시하는 것이다. - 직접적으로 표현하는게 아닌, 확률적으로 표현함.
* 완벽한 모션을 할 수 없기 때문에, 진짜 세상을 기준으로 하면 큰일 날 수 있음. - 대략적으로 이정도 위치에 있을 확률이 몇이다.

### 확률과 통계의 기본
* 기본

![image](https://user-images.githubusercontent.com/55529455/169981201-01c9fc31-cfe1-4eae-91d8-2713f26889ec.png)
* P(A) = P(A)가 참일 확률을 표현

* Discrete random variable
* 어떤 변수가 랜덤한 값을 가지는 가능성의 수가 정해져있는 걸 의미함.

![image](https://user-images.githubusercontent.com/55529455/169981918-790fa6fb-fd49-4f78-b87a-91bbd8da46e6.png)
* x1 ~ xn 까지의 모든 수를 더하면 1
* P() - probability math function

* Continuous random variable
* 연속되는 함수로 표현이 됨. - x 변수의 특정 x가 들어갈 수 있는 확률을 적분을 통해서 확률값을 표현
* P() - probability density function

![image](https://user-images.githubusercontent.com/55529455/169982446-323ca710-27b0-4dc7-a8b3-fddddaca9bc0.png)

* 변수가 여러개인 경우는?
* Joint, Conditional probability로 표현함.
* P(x, y) = 두개의 변수 x, y가 있을 때, X가 x를 취하고, Y가 y를 취할 확률을 표현
* 서로의 확률에 독립적이라면, P(x, y) = P(x)P(y)로 표현이 가능함. (단순히 곱한 값) - Joint
* P(x|y) = Y가 주어졌을 때, X의 확률분포를 뜻함. - conditional
* 만약 X와 Y가 독립적이면, P(x|y) = P(x)

![image](https://user-images.githubusercontent.com/55529455/169982608-5a31c52e-d999-4cc4-8f6e-c7c12b8cb217.png)

* Bayes rule 베이즈 법칙

![image](https://user-images.githubusercontent.com/55529455/169983652-a7410299-dc8d-45a0-913f-4210a8d138b2.png)
![image](https://user-images.githubusercontent.com/55529455/169984250-a974f2ef-b5ee-4d9d-bbff-bcb5a9ced2a6.png)

* 이는 SLAM에서 가장 중요하게 되는 요소임.
* y = 센서, x = 위치라고 하면, P(x|y) = 센서값이 주어졌을 때, 자신의 위치의 확률이라고 표현 할 수 있는 것.
* evidence = 센서의 값, prior = 힌트 (로봇의 위치, 지난 로봇의 위치)
* likelihood = P(y|x) (x가 주어졌을때, y의 분포확률) - 현재로봇위치 x가 주어졌을 때, 센서 값 y가 나올 확률
* 3개의 정보를 조합하게 되면, P(x|y)를 구할 수 있다. 여기서 x와 y의 순서를 마음대로 바꾸더라도, 식이 유지가 된다는 것이다. (베이즈 법칙)

## CMAKE Primer
* CMAKE - 크로스플랫폼 (아무 플랫폼에서 사용 할 수 있다.), 무료 오픈소스 소프트웨어, 자동 빌드, 테스팅, 패키징, 설치를 해줌. 컴파일러와 독립적인 작동
* CMAKE - 빌드를 해주는 주체가 아닌, 어떤 타겟 시스템에서 작동할 수 있게 커맨드를 해주는 시스템
* CMAKE - 복잡한 폴더 구조를 풀어줄 수 있고, 앱들마다 다양한 라이브러리를 구조적으로 해결 해줄 수 있음.
* CMAKE - 다양한 기존적인 빌드 환경 시스템에 잘맞고, 다른 종속성없이 C++ 컴파일러와 빌드 시스템만 있으면 된다.
* 플랫폼이 중요한 이유 : 우리가 목표로 잡는 시스템이 어떠한 플랫폼인지 이해해야함. (amd64(x86), arm64 하드웨어 플랫폼이나 mac, window SW 플랫폼 등)

* build 3rd party libraries from source - python 처럼 pip가 없다.
* Make C++ project - load your haeder, source file | Load 3rdparty libraries | configure output executables, libraries

## 선형대수 Primer
* Vector
* computer vision = list of variable, list of values - vector\<int\> vec = \{1, 2, 3\}
* physics = vector : object with magnitude and direction (F = ma)
* Mathematics = vector : A coordinate in space (x, y, z) in 3D Euclidean space

* Matrix
* Collection of vectors
* vector = 1D, Matrix = 2D
* Matrix = A map from a vector to another

![image](https://user-images.githubusercontent.com/55529455/170010172-7c51d93b-fa17-4bf3-8316-b3c68154fb48.png)
![image](https://user-images.githubusercontent.com/55529455/170025301-63c0b1f2-be56-4091-b204-424182fafa90.png)
![image](https://user-images.githubusercontent.com/55529455/170025333-df5e718d-56bc-48d1-bcee-2559a45f4cf7.png)
![image](https://user-images.githubusercontent.com/55529455/170025385-1c8dbd25-c35f-423c-a041-370fe264a4cf.png)
![image](https://user-images.githubusercontent.com/55529455/170025431-0f34130a-291d-49ec-a1e9-f125b45c2582.png)

* Matrix decomposition
* schur, LU, QR, Cholesky
* Composite matrix -> Factorized matrices

* SVD
* U, S, V^T로 표현함
* U, V^T 꽉찬 dense
* S 는 대각행렬

![image](https://user-images.githubusercontent.com/55529455/170025690-cdb6d04e-a3d7-4398-8b0b-fff4f2c9e24f.png)





