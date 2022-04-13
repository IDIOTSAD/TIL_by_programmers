# 강의 요약

> 기계학습에서 수학의 역할
> 수학은 목적함수를 정의하고, 목적함수의 최저점을 찾아주는 최적화 이론 제공
> 최적화 이론에 학습률, 멈춤조건과 같은 제어를 추가하여 알고리즘 구축
> 사람은 알고리즘을 설계하고 데이터를 수집
> 규칙(target)을 수학적 특징을 ㅗ보면 받아들이는 것이 수치적, 수학적으로 형태를 가짐.
> 전반적인 부분이 수학에 기반되어 있음

![image](https://user-images.githubusercontent.com/55529455/163099104-cbc778ff-c7b6-44d3-ab9f-6e61b8321c7f.png)
> 선형대수
> 기계학습을 이해하기 위한 관련된 기본 선형대수를 확인
> 수치화된 대상으로 받아들이기 때문에(벡터) - 연산을 통해서 결과값을 유추 (공간적인 이해를 위함)

> 벡터
> 샘플을 특징 벡터(입력 벡터)로 표현
> 요소의 종류와 크기 표현 (\[요소, 요소])
> 데이터 집합의 여러개 특징 벡터를 첨자로 구분함.

![image](https://user-images.githubusercontent.com/55529455/163099637-7cdc108d-a6b3-4dfe-89e0-ba003ebbcc43.png)
> 행렬
> 여러개의 벡터를 담음
> 요소 xij (i행 = xi, , j열 = x,j)
> 훈련집합을 담은 행렬을 설계 행렬이라 부름

![image](https://user-images.githubusercontent.com/55529455/163100560-c86cec46-86a2-44c9-a404-50f8e559c296.png)
> 행렬을 이용하면 방정식 (방정식계)를 간결하게 표현 가능

![image](https://user-images.githubusercontent.com/55529455/163101124-4572002f-43f4-4731-bf27-0c6fa7300ec8.png)
![image](https://user-images.githubusercontent.com/55529455/163101439-6888f859-08d5-408f-a59f-bc6122f49764.png)
![image](https://user-images.githubusercontent.com/55529455/163102046-705c3f9d-3f26-4066-95c0-65008b25d4f2.png)
> 행렬의 곱셈은 공간의 변화

> 텐서
> 3차원 이상의 구조를 가진 숫자배열 = RGB 숫자 컬러 영상
> 0차 = 수(스칼라)
> 1차 = 벡터
> 2차 = 행렬
> 고차원..

![image](https://user-images.githubusercontent.com/55529455/163104874-f95e2523-03d2-4b25-a807-ddea3f220703.png)
> 유클리디안, 맨해튼 디스턴스로 구분할 수 있음.
> 각도의 차이로 유사도를 판단할 수 있음.

![image](https://user-images.githubusercontent.com/55529455/163104955-716ed0f2-992e-46e4-9a65-fa6abf0e954c.png)
> 놈은 벡터와 행렬의 거리차를 의미함.

> 1차 놈과 2차 놈의 비교 - 놈의 사용법
> 거리(크기)를 사용 할 때
> 규제를 사용 할 때 (이동을 자유롭게 못하게 제한)

> 퍼셉트론
> 1958년 고안한 분류기 모델 - 활성함수 타우로는 계단 함수 사용

![image](https://user-images.githubusercontent.com/55529455/163105527-2e80fdbf-d4d1-4b01-abad-bcb46725d909.png)
![image](https://user-images.githubusercontent.com/55529455/163105942-865836f5-75da-4a6a-817f-6cb3d8d11666.png)
![image](https://user-images.githubusercontent.com/55529455/163106027-fc436c9e-7a1c-4919-a0c6-371f4e5ee1ef.png)
![image](https://user-images.githubusercontent.com/55529455/163106623-6282542f-e432-4796-b112-676ac3d2e53a.png)

> 내가 주어져있는 데이터값을 일정값을 기준으로 필터링 하겠다는 의미


















