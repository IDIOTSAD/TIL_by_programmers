# 강의 요약

> * 허프 변환 직선 검출
> * 2차원 영상 좌표에서의 직선의 방정식을 파라미터 공간으로 변환하여 직선을 찾는 알고리즘

![image](https://user-images.githubusercontent.com/55529455/160054136-64b7ab93-a7bc-48aa-a17d-d6030636c69e.png)
![image](https://user-images.githubusercontent.com/55529455/160054630-0626770e-7b20-49c1-a12a-042dcad6bacd.png)
> * 축적 배열 = 직선 성분과 관련된 원소 값을 1씩 증가시키는 배열 = 호프 변환
> * 각각의 점에대해서 좌표를 그려서 카운트를 증가시켜서 피크를 크게 만들고, 특정한 점에서 피크가 크게 튀는 구간이 a와 b 구간이 된다는 것.
> * 2차원 행렬 형태로 표현함. -> 여기서는 그래프로 표현을 하였음.

> * 직선의 방정식 y = ax + b를 사용할 때 의 문제점
> * 무한대로 가기 때문에 표현하기 어려움(수직, 수평으로 이루어진 선)
> * y축과 평행한 수직선을 표현하지 못함 = 극좌표계 직선의 방정식을 사용함.

![image](https://user-images.githubusercontent.com/55529455/160054990-d62cbd5f-2676-4e7f-9aaf-e4bd8f47ee8d.png)
![image](https://user-images.githubusercontent.com/55529455/160055405-90ea8bf3-3a89-423b-8732-79599b799207.png)


