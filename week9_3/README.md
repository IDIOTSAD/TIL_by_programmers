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

![image](https://user-images.githubusercontent.com/55529455/163117032-7fa17158-fe8c-475c-93a7-79f371d64a6f.png)
![image](https://user-images.githubusercontent.com/55529455/163117057-584cadc4-6dbc-4da3-b2ef-8e17d47d7a7d.png)

> 정리
> A는 역행렬을 가진다, 즉, 특이 행렬이 아니다
> A는 최대계수를 가진다
> A의 모든 행이 선형독립이다
> A의 모든 열이 선형독립이다
> A의 행렬식은 0이 아니다
> AtA는 양의 정부호 대칭행렬이다
> A의 고윳값은 모두 0이 아니다

![image](https://user-images.githubusercontent.com/55529455/163117224-c441214f-a884-4a67-acfe-9f9ba03b0cd1.png)
![image](https://user-images.githubusercontent.com/55529455/163117249-3b2b791b-e9e4-4eb7-b6e6-5d7216e6905e.png)
![image](https://user-images.githubusercontent.com/55529455/163117274-25a93f03-8260-4df9-8d2a-842effb9d268.png)
![image](https://user-images.githubusercontent.com/55529455/163117306-ed373ab1-1b8e-4ac4-8b9d-d14ec62532ea.png)
![image](https://user-images.githubusercontent.com/55529455/163117324-d275a516-848a-480e-878e-e8272b278306.png)
![image](https://user-images.githubusercontent.com/55529455/163117364-ca5867d0-09af-4ff8-97b5-b995f6867faa.png)
![image](https://user-images.githubusercontent.com/55529455/163117393-7080d771-d4dc-4d08-985b-dc3a7244cacb.png)

> 기계학습이 처리해야할 데이터는 불확실한 세상에서 발생하므로, 불확실성을 다루는 확률과 통계를 잘 활용해야 함.

> 확률변수 (윳)
> 다섯가지 경우 중 한 값을 갖는 확률변수 x->x의 정의역 (도, 개, 걸, 윳, 모)

![image](https://user-images.githubusercontent.com/55529455/163126593-3001e4ef-07f8-4dbd-bed8-7711f2148912.png)
![image](https://user-images.githubusercontent.com/55529455/163126847-826a0218-1371-4a08-a0d7-221416ed6427.png)
![image](https://user-images.githubusercontent.com/55529455/163127218-f6101b88-00d8-4fc1-87f4-d4a98d84df66.png)
![image](https://user-images.githubusercontent.com/55529455/163127268-d94781db-2ba1-4451-8716-27c7ab80e213.png)
![image](https://user-images.githubusercontent.com/55529455/163127346-c8a37dae-e17b-4f48-9e6f-a5857c80a692.png)

> 데이터를 보고 그럴 것이다 추정하는 것 = 우도 (실제 상황에서는 우도는 쉽게 구할 수 있고, 확률분포는 구하기 힘듬)

![image](https://user-images.githubusercontent.com/55529455/163128941-646f4205-e1cc-48b1-b215-ebea45ef1d91.png)
> 기계학습에서 사후확률을 직접적으로 푸는건 불가능하니 사전확률과 우도를 이용해서 문제를 해결하겠다는 뜻.
> 우리가 대상을 카운트 할 수 있으므로 사전확률을 계산하는것은 해결이 가능함.

![image](https://user-images.githubusercontent.com/55529455/163129336-2ccac255-9c4c-4bcc-a5e0-728578e077ef.png)
> 데이터로 부터 사전확률을 찾을 순 있지만, 관찰값이지 정확한 값은 아님.

![image](https://user-images.githubusercontent.com/55529455/163129447-32f369b4-5f5a-4e9b-9115-61994500ca46.png)
> 우도는 다시 정리하면, 내가 확률 분포를 설명하기 위해서 내가 가지고 있는 데이터를 설명하기 위해 대리로 만드는 것.
> 확률 분포를 설명할 수 있는 매개변수를 설명해주는 것.

![image](https://user-images.githubusercontent.com/55529455/163129634-bda93a18-87bf-456b-a9fd-f2b6dd446ecc.png)
![image](https://user-images.githubusercontent.com/55529455/163129696-9251257c-8803-4cb4-90a1-6cf1c6ccb873.png)
![image](https://user-images.githubusercontent.com/55529455/163129708-e492acf2-ee55-4df3-90e4-b088faf33d29.png)
![image](https://user-images.githubusercontent.com/55529455/163129728-76983a23-27d1-45a9-98f0-64518f1527a5.png)
![image](https://user-images.githubusercontent.com/55529455/163129752-db0d481e-ce88-4029-8774-588e92c468bf.png)
![image](https://user-images.githubusercontent.com/55529455/163129790-2def0d42-970a-49df-9625-646437249ccf.png)

> 정보이론과 확률통계는 많은 교차점을 가짐
> 확률 통계는 기계학습의 기초적인 근간 제공 (해당 확률 분포 추정, 확률 분포 간의 유사성 정량화)
> 정보이론 관점에서도 기계학습을 접근 가능 - 불확실성을 정량화 하여 정보이론 방법을 기계학습에 활용한 예
> 예시 : (엔트로피, 교차 엔트로피, KL발산 (상대 엔트로피)

> 정보이론 : 사건이 지닌 정보를 정량화 할 수 있는가? = 아침에 해가 뜬다와 오늘 아침에 일식이 있었다라는 정보중 어떤게 정보가 많은가?
> 정보이론의 원리 = 확률이 작을수록 많은 정보를 지님. 자주 발생하는 사건보단 잘 일어나지 않는 사건의 정보량이 더 많음.

> 자기정보 = 사건의 정보량 (단위 : 2아래인 경우는 비트, 로그의 밑이 자연상수이면 nat 나츠)
> 엔트로피 = 확률변수 x의 불확실성을 나타태는 엔트로피, 모든 사건 정보량의 기대 값으로 표현

![image](https://user-images.githubusercontent.com/55529455/163143592-3c1f1c02-4656-4c0e-97e4-e481ccff5bd1.png)
![image](https://user-images.githubusercontent.com/55529455/163143637-6205afa3-1c70-455b-989b-4eacf2991e7d.png)
![image](https://user-images.githubusercontent.com/55529455/163143680-94cf7c58-a3df-48ba-8ddf-75d673838c23.png)
![image](https://user-images.githubusercontent.com/55529455/163143734-7595d217-4e01-496e-bd85-5d6362975535.png)
> 내가 원하는 데이터 확률과 모델에서 나오는 데이터 확률을 둘 다 동일해지도록 맞춰야함.
> 실제 확률분포와 내가 생각하는 확률분포의 오차를 낮춰야한다.
> 교차 엔트로피를 낮춘다 = K 오차를 낮춘다는 것.

![image](https://user-images.githubusercontent.com/55529455/163164490-1b0d9f07-83e2-46b8-8e96-4d0d1cd7eafd.png)
> 순수 수학 최적화와 기계학습 최적화의 차이
> 기계 학습의 최적화는 단지 훈련집합이 주어지고, 훈련집합에 따라 정해지는 목적함수의 최저점을 만드는 모델의 매개변수를 찾아야함.
> 주로 SGD(확률론적 경사 하강법) 사용함. - 손실함수 미분하는 과정 필요 -> 오류 역전파 알고리즘

![image](https://user-images.githubusercontent.com/55529455/163165327-ad05c4fc-6bf2-4c03-8e7e-6956be706f14.png)
![image](https://user-images.githubusercontent.com/55529455/163165355-90f61d25-a156-4e16-adea-4071d9e6c298.png)
![image](https://user-images.githubusercontent.com/55529455/163165390-f6271517-ec62-45e0-98d1-21e493c8d26e.png)
![image](https://user-images.githubusercontent.com/55529455/163165417-e039a022-7b6a-4f28-b48a-1f38d9d9a5f6.png)

> 독립변수와 종속변수의 구분
> 식에서 일반적으로는 x는 독립변수, y는 종속변수 -> y = wx + b
> 기계학습에서 예측단계를 위한 해석은 무의미

> 최적화는 예측단계가 아니라 학습 단계에 필요

![image](https://user-images.githubusercontent.com/55529455/163166187-842d7a75-dcb5-42e8-a0cb-641e96a7588b.png)
![image](https://user-images.githubusercontent.com/55529455/163166222-9fa205bc-6a43-44ce-a7d4-d05b37a99c5f.png)
![image](https://user-images.githubusercontent.com/55529455/163166252-b716ebe6-5c73-4130-b09f-c380fc6ebaf9.png)
![image](https://user-images.githubusercontent.com/55529455/163166295-757d3d08-73da-4bb8-975a-2eba11ed9d66.png)
![image](https://user-images.githubusercontent.com/55529455/163166321-a141311e-ffcc-4dab-ae59-a8dcdcf2724c.png)
![image](https://user-images.githubusercontent.com/55529455/163166362-f3329329-b2fc-4df9-a93b-d44f9c5d5054.png)





















