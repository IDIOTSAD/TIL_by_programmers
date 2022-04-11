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





