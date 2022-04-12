# 강의 요약

> * HW 중심에서 SW의 중심으로 흘러가고 있음
> * ex) 자동차 산업 = 하드웨어 중심이었다가 테슬라의 등장으로 SW의 중요성으로 두각됨.
> * 혁명의 시작 - 인공지능 혁명

> * 인공지능 - 인간의 학습능력과 추론능력, 지각능력, 자연언어의 이해능력 등을 컴퓨터 프로그램으로 실현한 기술
> * 인간처럼 생각하고 행동하는 기기의 탄생
> * 인간도 학습이 중요함 - 머신러닝의 중심인 학습. 인공지능 요소 중 머신러닝이 있고, 그 안에 딥러닝(하나의 학습방법)이 있음
> * 인공지능하면 생각나는 것? - 알파고
> * 일상 속 인공지능 - 음성인식, 추천 시스템, 자율주행, 실시간 객체 인식, 로봇, 번역
> * 인공지능 - 기기가 사람처럼 행동 할 수 있도록 - 1940년부터 지금까지 꾸준히 개발되었음.
> * 1940 ~ 1960 인공지능 초반 - 엘런 튜닝 (이미테이션 게임) => 인공지능의 시작을 알린 촉발의 시대
> * 1980 ~ 2010 => 기계학습의 번창 시대, 학습과정을 통해 문제를 해결하겠다 - 잘 되지 않음
> * 2010 ~ 현재 => 알고리즘, 방법론이 많이 나옴으로써 심층학습의 혁신으로 인공지능 황금시대가 만들어짐.
> * 인공지능을 하려면, python과 open source로 많이 해야 함.
> * 인공지능 구현은 레고처럼 조립할 수 있음 = 이를 도와주는 프레임워크 (카페, 파이토치, 텐서플로)
> * 인공지능은 도구임. 도구를 만드는 방법도 중요하지만, 사용 방법에 대해서도 중요함.
> * 기술에 대한 부분에서 유용하게 사용하면 도움이 되지만, 유용하게 사용하지 않으면 무기가 될 수 있음.

> * 사람/동물의 학습
> * 수학, 과학, 역사 등 사고 영역 + 수영, 자전거 등 행위 영역
> * 파블로프의 개 실험

> * 기계학습
> * 기계도 학습이 가능한가? = 완벽하게는 아니지만 가능하다
> * 경험을 통해서 점진적으로 성능이 향상되는 기계를 만들 수 있다.

> * 인공지능의 사전적 의미 = 인간의 학습능력과 추론능력, 지각능력, 자연언어의 이해능력 등을 컴퓨터 프로그램으로 실현한 기술
> * 학습의 사전적 의미 = 경험의 결과로 나타나는 비교적 지속적인 행동의 변화와 그 잠재력의 변화 또는 지식을 습득 하는 과정
> * 기계학습이란? 경험을 통해 배우는 프로그래밍
> * 어떤 컴퓨터 프로그램이 T라는 작업을 수행한다. 이 프로그램의 성능이 P라는 척도로 평가 되었을 때, 경험 E를 통해 성능이 개선된다면 학습을 한다고 할 수 있음.
> > * 사례 데이터, 과거 경험을 이용하여 성능 기준을 최적화 하도록 프로그래밍
> * 성능을 개선하거나 정확하게 예측하기 위해 경험을 이용하는 계산학 방법들

> * 최적의 알고리즘(프로그램)을 찾는 행위
> * 경험 E를 통해, 주어진 작업 T에 대한 성능 P의 향상 = 3가지에 대해서 정의를 내려야하고, 학습을 진행해야함.

> * 기계학습과 전통적인 프로그래밍의 비교
> * 기존의 프로그래밍 = 입력을 주고, 규칙에 의해서 결과를 찾아가는 것. 연속적으로 나열, 서술
> * 기계 학습 = 입력과 원하는 결과를 주면, 규칙을 찾는 것.

> * 인공지능의 탄생 = 연산장치의 탄생
> * 컴퓨터의 뛰어난 능력, 복잡한 연산을 사람보다 잘함
> * 컴퓨터에 대한 기대감 = 컴퓨터의 능력 과신
> * 사람의 지능행위를 컴퓨터가 모방할 수 있을까에 대한 호기심 = (개와 고양이)
> * 1940년대 인공지능 개념 정의 및 분야 대두

> * 초창기 지식기반 방식 주류 = 모든 지식과 규칙을 알려주는 것.
> * 지식기반 : 경험적인 지식 혹은 사실을 인위적으로 컴퓨터에 부여하여 학습
> * 큰 깨달음 = 지식기반의 한계 - 학습의 대상이 심한 변화 양상을 가진 경우, 모든 지식 혹은 사실의 나열은 불가능
> * 데이터가 어려워지는 경우 문제가 발생.

> * 인공지능의 주도권 전환
> * 지식기반 - 기계학습 - 심층학습(표현학습)
> * 데이터 중심 접근 방식으로 전환
> * 점점 사람을 모방하고 있음.

> * 간단한 기계 학습 예제
> * x는 시간, y는 물체 물체가 이동하는 시간에 비례해서 얼마만큼 멀어졌는지 체크.
> * 시간 대비해서 얼마나 그 물체가 이동했는지를 거리를 측정하는 것이 y
> * 이러한 데이터를 보고 문제를 풀고 싶음. - 컴퓨터는 정형화 시켜놓고 행렬이나 벡터로 변환해서 이해함.
> * 기계학습에 필요한 요소 - 경험, 과업, 성능 (ETP)
> * y값은 회귀 할 때는 연속되는 실수값, 분류할 때는 부류 혹은 종류의 값 (고양이, 개의 값 - 분류, 점 4개를 주고 예측 - 회귀)

![image](https://user-images.githubusercontent.com/55529455/162886911-6ba9b436-03a5-4f4f-9c30-e6423eda8426.png)

> * 훈련 집합
> * 가로축은 특징, 세로축은 목표치
> * 관측한 4개의 점이 훈련 집합을 구성함 (관찰된 값을 의미 - 훈련데이터)
> * 데이터는 추론데이터와 훈련데이터로 구분됨.
> * 4개의 데이터는 각각 대응되는 데이터로 구성되어 있음.
> * 눈에 보이지 않지만, 선을 만드는 규칙이 내재되어 있다는 것을 알 수 있음.
> * 훈련집합은 데이터(경험)에 원래 오리지널한 규칙이 생성되어있다는 것을 알아야 한다. (랜덤하지 않음)

![image](https://user-images.githubusercontent.com/55529455/162888246-e9f43d51-98d9-444f-b26d-94c0c590628e.png)

> * 관찰된 데이터들을 어떻게 설명할 것인가?
> * 가설 = 눈대중으로 데이터 양상이 직선형태를 보임. -> 모델을 직선으로 선택 가정.
> * 2개의 매개변수 w와 b => y = wx + b -> 여기서 w와 b를 찾는 것 (규칙을 찾는것)

> * 기계학습의 훈련
> * 주어진 문제인 예측을 가장 정확하게 할 수 있는 최적의 매개변수를 찾는 작업
> * 처음은 임의의 매개변수 값에서 시작하지만, 개선하여 정량적인 최적 성능에 도달
> * 잘 모르지만 임의의 점을 그었다. = 우리가 평가 할 때, 4개의 점을 f1이라는 것으로 설정하고 싶음
> * f1에서 나오는 예측값은 그래프에서 확인 할 수 있음. = 실제 관측된 값과 근접하지 않음.
> * 갱신하거나 점진적으로 훈련을 통해서 바꾸어 f2, f3 로 바뀌면서 점차 찾게 됨.
> * 실제 훈련 집합이 얼마나 차이나는지에 대한 오차 = 에러라고 함. (손실함수)

![image](https://user-images.githubusercontent.com/55529455/162922641-0c0922d8-bc2a-4ca1-bff5-9d1bf7280264.png)

> * 훈련을 마치면 추론을 수행
> * 새로운 특징에 대응하는 목표치의 예측에 사용
> * 기계학습의 궁극적 목표
> * 훈련집합에 없는 새로운 데이터에 대한 오류를 최소화 (새로운 데이터 = 테스트 집합)
> * 테스트 집합에 대한 높은 성능을 일반화 능력이라 부름 (모의고사만 잘 본 학생 vs 모의고사와 수능을 잘 본 학생)

> * 기계학습의 필수요소
> * 학습할 수 있는 데이터가 있어야함.
> * 데이터 규칙 존재
> * 수학적으로 설명 불가능 = 데이터가 있을 때, 노이즈 때문에 실제 값들이 바뀔 수 있음

![image](https://user-images.githubusercontent.com/55529455/162925023-f64708dd-47c5-4910-9f01-e1dae21e4f42.png)

> * 특징공간의 이해
> * 1차원과 2차원 특징 공간

![image](https://user-images.githubusercontent.com/55529455/162935874-71dc09df-b54f-456e-b29e-8735fd8e91fa.png)
![image](https://user-images.githubusercontent.com/55529455/162935952-efe884b4-7d5d-4f33-8906-fff7e0bbaff3.png)
![image](https://user-images.githubusercontent.com/55529455/162936001-8ef951b2-a69a-40a6-a468-7753b211a15f.png)
![image](https://user-images.githubusercontent.com/55529455/162936939-5d087128-5431-4810-b1d9-d5260c26218d.png)
![image](https://user-images.githubusercontent.com/55529455/162937140-e60a3f32-a8cc-42ca-aeaa-4f8893243e5b.png)
![image](https://user-images.githubusercontent.com/55529455/162937255-bc2ed69b-ac92-435c-881e-d6f28ae4ff10.png)

> * Ada Lovelance 여사의 통찰력 = 해석기관은 숫자 이외의 것도 처리할 수 있다.
> * 200년이 지난 지금, 인간수준의 사진 인식 능력, 알파고는 바둑으로 사람의 능력을 압도, 구글사의 듀플렉스는 인간과 대화

> * 인공신경망의 역사
> * 1940 - 1960 = 인공두뇌학
> * 1980 - 1990 = 결합설
> * 2006 - 현재 = 심층학습

> * 기계학습 알고리즘과 응용의 다양화
> * 표현 학습이 중요해짐
> * 심층 학습이 기계학습의 주류
> * 심층학습은 현대 인공지능 실현에 핵심 기술

![image](https://user-images.githubusercontent.com/55529455/162939173-71ab9e3f-73a4-4ebb-878d-37fb6b5797e3.png)
![image](https://user-images.githubusercontent.com/55529455/162939366-6e0cc7d8-ff70-4fc9-8b85-24198625cfb8.png)
![image](https://user-images.githubusercontent.com/55529455/162939427-e72ee21a-73b7-46a4-8341-13fdb89c878d.png)
![image](https://user-images.githubusercontent.com/55529455/162939581-8b0b24f6-7abb-4dfb-acec-d6899e53db2d.png)

> * 데이터의 적은양 = 차원의 저주와 관련
> * MNIST = 28 * 28 단순히 흑백으로 구성된다면 서로 다른 총 샘플 수는 2^784 가지지만, MNIST는 6만가지의 샘플

> * 적은 양의 데이터베이스로 어떻게 높은 성능을 달성하는가?
> * 방대한 공간에서 실체 데이터가 발생하는 곳은 매우 작은 부분 공간임
> * 데이터 희소 특성 가정
> * 매니폴드 (마나+끼다) 가정
> * 고차원의 데이터는 고나련된 낮은 차원의 매니폴드에 가깝게 집중되어 있음.
> * 일정한 규칙에 따라 매끄럽게 변화.

![image](https://user-images.githubusercontent.com/55529455/162940790-50be053f-472d-40ae-8831-96309cc114a5.png)

> * 4차원 이상의 초공간은 한꺼번에 가시화 불가능
> * 여러가지 가시화 기법 - 2개씩 조합하여 여러개의 그래프 그림
> * 고차원 공간을 저차원으로 변환하는 기법들

![image](https://user-images.githubusercontent.com/55529455/162941453-035644c7-523f-402d-8822-b71fca2ea41c.png)
![image](https://user-images.githubusercontent.com/55529455/162941609-f88ef29a-108a-4601-b182-0020108f5517.png)
![image](https://user-images.githubusercontent.com/55529455/162941677-db3503ba-61ec-46bc-bd02-bcafeca4c533.png)
![image](https://user-images.githubusercontent.com/55529455/162941712-9971547c-066e-49f1-8d30-e72046f6552e.png)
![image](https://user-images.githubusercontent.com/55529455/162941745-f8b6ab71-12e7-49ce-9f72-55446dde1b56.png)
![image](https://user-images.githubusercontent.com/55529455/162941782-efd3a35b-0c8a-41da-b848-9b5f1fe48e78.png)
![image](https://user-images.githubusercontent.com/55529455/162941817-5b253bbb-a842-41ca-bbe2-b640d686abf2.png)
![image](https://user-images.githubusercontent.com/55529455/162941935-b978bed3-d752-4547-b215-c4d0a134d5bc.png)
![image](https://user-images.githubusercontent.com/55529455/162942942-36ad75bd-e7b3-49ee-948a-a0bda67ab5c8.png)
![image](https://user-images.githubusercontent.com/55529455/162942978-d3744779-2583-4b3d-b010-01b9e7025a04.png)
![image](https://user-images.githubusercontent.com/55529455/162942993-6b21f90e-24d8-40c9-a37f-8509687cabe0.png)
![image](https://user-images.githubusercontent.com/55529455/162943017-1f729847-27aa-4ae9-a3e5-0178511d03d4.png)
![image](https://user-images.githubusercontent.com/55529455/162943045-df7a2116-1d2b-4a4a-86c8-4ef599611d5d.png)
![image](https://user-images.githubusercontent.com/55529455/162943074-091a3f82-3442-4f1b-9cb4-98d4930b6b9b.png)
![image](https://user-images.githubusercontent.com/55529455/162943101-9ac42b4c-7d0f-424d-ae89-f17b12677382.png)
![image](https://user-images.githubusercontent.com/55529455/162943126-cbc118f5-7069-4a67-acd3-332630a7686b.png)
![image](https://user-images.githubusercontent.com/55529455/162943149-529dd302-2b2c-4e1c-8a4f-b7696ac502a6.png)
![image](https://user-images.githubusercontent.com/55529455/162943174-2c366a2e-baa5-4e16-a6bd-ac1bfd544da0.png)
![image](https://user-images.githubusercontent.com/55529455/162943202-ff089191-1222-45af-9685-6d437c5ae558.png)
![image](https://user-images.githubusercontent.com/55529455/162943223-9ec5888c-c898-4869-a177-359f40c0a4f8.png)
![image](https://user-images.githubusercontent.com/55529455/162943244-df18ad0b-9f9b-4d23-b402-2010916590eb.png)
![image](https://user-images.githubusercontent.com/55529455/162943271-3d181a96-6017-42ac-bd86-2ceadb442ec8.png)
![image](https://user-images.githubusercontent.com/55529455/162943294-1d4dae85-8c16-497e-97a7-0737b599b232.png)
![image](https://user-images.githubusercontent.com/55529455/162943345-1d397d60-0c89-49cd-bd00-499d3c114092.png)
![image](https://user-images.githubusercontent.com/55529455/162943434-507fe883-b71d-42c6-a3d6-47131d2ac7ae.png)
![image](https://user-images.githubusercontent.com/55529455/162943466-f5680c24-52ce-41d3-bf75-f2f1cd14f2d8.png)
![image](https://user-images.githubusercontent.com/55529455/162943508-6ee6f439-48b2-4fca-8f21-e7af9041ac0a.png)
![image](https://user-images.githubusercontent.com/55529455/162943538-e0d478ef-cf09-4a80-a601-c599ae6ade75.png)

