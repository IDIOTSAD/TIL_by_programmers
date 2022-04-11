# 강의 요약

> * Numpy 시작하기
> * import numpy as np

> * % = 매직 키워드, 주피터노트북에서 뭘 한다는 뜻.

> * numpy를 사용해야하는 이유
> * 일반 arry를 사용하면 마이크로세크가 나옴, 하지만 numpy를 사용하면 나노세크가 나옴.
> * numpy가 훨신 빠름

> * numpy의 array
> * np.array(\[1,2,3])
> * array는 차원별로 띄어쓰기를 해서 print 해줌.
> * array.shape => 자료의 n차원을 출력해줌.

> * 벡터와 스칼라 사이의 연산
> * 벡터의 각 원소에 대해서 연산을 진행함.
```
x = np.array(\[1,2,3])
c = 5
x + c => [6 7 8]
x - c => [-4 -3 -2]
```

> * 벡터와 벡터 사이의 연산
> * 벡터의 같은 인덱스 끼리 연산이 진행됨.
```
x = np.array([1,3,5])
y = np.array([2, 9, 20])
x + c => [3 12 25]
x - c => [-1 -6 -15]
```

> * array의 indexing
> * 배열에서 특정 위치의 원하는 원소를 가지고 오고 싶으면? = python의 리스트와 유사하게 진행.
```
x = np.array([1,3,5])
print(x[a][b]) => a행 b열의 값을 가지고 옴.
```


> * array의 slicing
> * 배열에서 특정 범위의 원하는 원소를 가지고 오고 싶으면? = python의 리스트와 유사하게 진행.
```
x = np.array([1,2,3,4,5],[1,2,3,4,5])
print(x[0:2][1:3]) => 0행~1행 1열 ~ 2열의 값을 가지고 옴. -> [2,3][2,3]이 나옴.
[:b] => 0 ~ b 까지
[a:] => a ~ 끝 까지
[:] => 처음부터 끝까지
```

> * array의 Broadcasting
> * Numpy가 연산을 진행하는 특수한 방법

![image](https://user-images.githubusercontent.com/55529455/162666047-81a84462-72a5-4630-a7ae-ac26f118790c.png)
![image](https://user-images.githubusercontent.com/55529455/162666092-c92eca33-1f83-4a69-93cb-c763b7d5def5.png)

> * 영벡터 (영행렬)
> * 원소가 모두 0인 벡터
> * np.zeros(dim)을 통해 생성

> * 일벡터 (영행렬)
> * 원소가 모두 1인 벡터
> * np.ones(dim)을 통해 생성

> * 대각행렬
> * Main diagonal을 제외한 성분이 0인 벡터 => (0,0), (1,1) ... (n,n)의 행렬을 제외한 성분이 0
> * np.diag(dim)을 통해 생성

> * 항등행렬
> * Main diagonal을 제외한 성분이 0인 벡터 => (0,0), (1,1) ... (n,n)의 행렬부분이 1이고 나머지 0
> * np.eye(dim)을 통해 생성

> * 행렬곱
> * 행렬간의 곱연산
> * np.dot(dim) 또는 @를 사용

![image](https://user-images.githubusercontent.com/55529455/162685686-b7e6afc8-3341-4cde-a06f-8be412622387.png)

> * 트레이스
> * Main diagonal의 합 => (0,0), (1,1) ... (n,n)의 행렬부분의 합
> * np.trace(dim)을 통해 생성

> * 행렬식
> * 행렬을 대표하는 값들 중 하나 = 선형 변환, ad - bc의 값.
> * np.linalg.det(dim)을 통해 생성
> * 3차원의 경우는 다음과 같음.

![image](https://user-images.githubusercontent.com/55529455/162685994-5dccae07-2c9c-4930-82a5-a9d80ac3c516.png)

> * 역행렬
> * 행렬 A에 대해 AB = BA = I를 만족하는 행렬 B = A^-1
> * np.linalg.inv(dim)을 통해 생성

![image](https://user-images.githubusercontent.com/55529455/162686121-dd3e5a01-d12b-41ba-9c54-33503e9cc81c.png)
![image](https://user-images.githubusercontent.com/55529455/162686162-d7597189-3100-4b6e-b97c-907377d402c7.png)

> * Matplotlib = 파이썬의 데이터 시각화 라이브러리
> * 라이브러리 = 개발자들이 만들었음. 라이브러리 내부에 있는 코드를 우리가 직접 하나하나 조합해야함.
> * 프레임워크 = 이미 만들어진 틀에서 내용물을 채워서 결과를 만듬
> * import matplotolib.pyplot as plt
> * %matplotlib inline
> * 자주 사용되는 plotting의 옵션
```
크기 = figsize
제목 = title
라벨 = _label
눈금 = _tics
범례 = legend
```
> * Matplotlib Case Study
```
꺽은선 그래프 = plot
산점도 = scatter plot
박스그림 = box plot
막대그래프 = bar chart
원형그래프 = pie chart
```
> * 더 멋진 그래프, seaborn case study
```
커널밀도그림
카운트그림
캣그림
스트립그림
히트맵
```

> * Case Study with Argments
> * plt.plot(\[1,2,3,4,5]) # 실제 plotting을 함. => 이렇게 하면 y = x+1 그래프가 그려짐
> * x는 자동적으로 list의 인덱스에 해당하고, y는 list의 value가 지정됨.
> * plt.show() # plt를 확인하는 명령
> * plt.figure() # plotting을 할 도면을 선언
> * figsize # 그래프의 도면 figure 인자를 figsize 함수를 이용하여 크기 조절이 가능
> * plt.figure(figsize=(6,6)) # figsize는 tuple 형식의 데이터를 주면 됨.

> * 2차원 그래프 그리기 (numpy 사용)
> * x = # 정의역 선언
> * y = # f(x) 선언
```
x = np.array([1,2,3,4,5])   #정의역
y = np.array([1,4,9,16,25]) #f(x)
plt.plot(x,y)
plt.show()
```
> * # np.arange(a,b,c) 시작점 a, 끝점 b, c (python은 int로 고정되어있음, numpy는 아님.)
```
x = np.arange(-10,10,0.01) 
plt.plot(x, x**2) # y는 x의 제곱
plt.show()
```
> * x축 추가설명 plt.xlabel("내용"), y축 추가설명 plt.ylabel("내용")
> * x, y축 범위를 설정하기 = plt.axis(\[a,b,c,d]) \[xmin, xmax, ymin, ymax] 구성
> * x, y축 눈금 설정 = (x축) plt.xticks(\[i for i in range(-5, 5, 1)]) (y축) plt.yticks(\[i for i in range(-5, 5, 1)])
> * range() 함수는 a ~ b-1까지의 범위이기 때문에, 이를 감안해서 range()를 설정해줘야 함.
> * 그래프에 title = plt.title("내용")
> * 범례 = plt.plot() 내부의 파라메터 label="내용" => ex) plt.plot(x, y, label = "내용")

> * 꺽은선 그래프 = plt.plot(x,y)
> * 산점도 = plt.scatter(x,y)
> * 박스 그림 = plt.boxplot(y), plt.boxplot((x,y))를 하게 된다면, box plot이 2개의 변수에 대한 box생성
> * 막대 그래프 = plt.bar(x,y)
> * 히스토그램 = plt.hist(y) = 도수분포를 직사각형의 막대 형태로 나타냄. 계급으로 나타낸 것이 특징 (0,1,2)가 아닌 0~2의 범주형 데이터로 구성 후 그림을 그림
> * 히스토그램 예시 = plt.hist(y, bins=np.array(0, 20, 2))
> * 원형 그래픅 = plt.pie(), 예시 = z = \[100,200,300,400] plt.pie(z, label=\["1", "2", "3", "4"])

> * Seaborn
> * Matplotlib를 기반으로 더 다양한 시각화 방법을 제공하는 라이브러리
> * import seaborn as sns

> * 커널밀도그림 = 히스토그램과 같은 연속적인 분포를 곡선화해서 그린 그림
> * sns.kdeplot() ex) sns.kdeplot(y, shade=True) shade는 내부에 색칠할지 여부

> * 카운트 그림 = 범주형 column의 빈도수를 시각화 -> Groupby 후의 도수를 하는 것과 동일한 효과
> * sns.countplot()

> * 캣그림 = 숫자형 변수와 하나 이상의 범주형 변수의 관계를 보여주는 함수
> * sns.catplot()

> * 스트립그림 = scatter plot과 유사하게 데이터의 수치를 표현하는 그래피
> * sns.stripplot()






















