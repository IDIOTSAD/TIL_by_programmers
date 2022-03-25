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
> * 구현 할 때, 신경써야하는 점
> * 바둑판 모양을 만들어서 검출하는데, 바둑판을 얼마나 촘촘하게 만들 것인가?
> * 곡선에서 1씩 증가시키는 구간이 빨라지게 될 것임. 하지만, 촘촘하게 한다면, 시간이 오래걸린다. 
> * 하지만, OpenCV에 구현되어 있기 때문에, 직접 구현하진 않아도 됨.

![image](https://user-images.githubusercontent.com/55529455/160055837-7774d458-55e9-4f6e-ad0b-97fe7f51bb47.png)
> * 허프 변환을 할 때, 시간이 너무 오래 걸리면, rho, theta의 간격을 조정하면서 해야한다. - 시간 검사는 필수
> * stn, srn은 디폴트 값을 주는게 좋을듯. 
> * 다만, min, max theta는 변환 시키는게 좋음. /\ 직선이나 || 직선을 골라서 검출하는데 필요함. 

![image](https://user-images.githubusercontent.com/55529455/160058138-e080eabf-e8f2-40dc-8114-e934ec157e27.png)
> * 위의 함수가 어렵기 때문에, P라는 함수가 제공됨.
> * 확률적(P) 허프 변환이라고 함.
> * 선분의 최소 길이를 지정하여 직선인지 판단할 수 있음.
> * 에지는 다 이어져서 나오는 것이 아니라 끊어져서 나오는 경우도 존재함. - 이럴 경우 maxLineGap을 주어 직선으로 간주하냐 마냐 (1개의 직선? 2개의 직선)

![image](https://user-images.githubusercontent.com/55529455/160060984-6349c4e7-7881-4cd1-8adc-5551a8713994.png)
> * threshold를 정하는 것이 중요. 정하는 방법으로는 전역 스레숄, 적응형 스레숄이 있음.
> * 매번 평균 계산하는 것은 번거로운 일임. 이를 해결하기 위해 otsu 알고리즘을 사용함.
> * otsu 알고리즘은 임의의 지점을 정해서 두 분류로 나누고, 두 분류의 값이 가장 평탄한 지역을 임계값으로 줌. (처음 임계값을 임의로 잡고)
> * 분산은 차이값의 평균을 계산하는 것. = 편차(값 - 평균)의 제곱의 평균
> * Image Quality Tuning 가 중요하다고 볼 수 있음.

> * 속도 향상을 위해 허프 그래디언트 메소드 사용
> * 입력 영상과 동일한 2차원 평면 공간에서 축적 영상을 생성
> * 에지 픽셀에서 그래디언트 계산
> * 그래디언트 방향에 따라 직선을 그리면서 값을 누적
> * 영상이 어두운 경우에는 일정 밝기 이상으로 끌어 올려야함. = 캐니에서 미분을 사용하는데, 편차가 적은 경우 안될 수 있음.
> * 2가지 방법이 존재, 1. 캐니의 범위를 조절함 (전체적으로 줄여줌) 2. 편차의 범위를 늘릴 수 있도록 함.(스트레칭 등) but 노이즈가 생길 수 있다.

![image](https://user-images.githubusercontent.com/55529455/160064614-54888993-04c3-4d5b-b622-ca02312f141c.png)
![image](https://user-images.githubusercontent.com/55529455/160065970-4c320902-9e22-4fb5-90ba-cc9ffe0859d0.png)
> * 메인 메모리에서 GPU 메모리로 옮기는 과정에서 시간이 걸릴 수 있음.
> * CPU는 좌표를 변환하면서 점을 찍을 수 있는 고급 기술을 가지지만, GPU는 점을 찍을지 말지에 대한 정도만 하지만, 코어 개수가 많기 때문에 한번에 처리함.

![image](https://user-images.githubusercontent.com/55529455/160067003-9aa4ce81-465f-44c2-9720-328ef1e06415.png)
> * add 함수 = a의 위치값 + b의 위치값을 더해서 c라는 위치값으로 만듬. = CUDA 커널 함수
> * 여기서 global은 쿠다가 설치되어있어야 해석 가능함.
> * cudaMalloc = 쿠다함수. = 변수 동적, Memcpy를 통해서 변수 복사 후, add 함수 수행.

![image](https://user-images.githubusercontent.com/55529455/160067425-77319731-fdb6-453c-97f0-c206cd11b494.png)
![image](https://user-images.githubusercontent.com/55529455/160067741-bc8560af-2e29-4113-8aff-3c886cf4e4cc.png)
![image](https://user-images.githubusercontent.com/55529455/160068465-aa176ce1-d8d5-485b-9dcf-373aeaf999a2.png)
![image](https://user-images.githubusercontent.com/55529455/160069352-150d60a5-ba48-4fa7-a748-1e72d496253d.png)





