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
















