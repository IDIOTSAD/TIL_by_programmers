# 강의 요약

> CNN - 컨벌루션 뉴럴 네트워크
> 컨벌루션 = 컨벌루션 행렬 3x3, 5x5 커널을 컨벌루션 연산을 수행하는 것.
> 이미지를 기하학적인 자료로 뽑는 것.
> 이미지 프로세싱의 커널의 종류는 많다.

> A의 input image에서 W의 컨벌루션 레이어(커널)에 컨벌루션 연산(인덱스끼리 곱해서 나온 값들의 합)을 통해서 1개의 output을 출력함.
> 슬라이딩 윈도우 처럼 하나하나 슬라이딩 하면서 값을 연속적으로 출력

> padding = 원본 이미지에 외각에 zero value를 넣어주는 것. 1개를 넣으면 외각에 1줄의 0을 만들어내고, 2개를 넣으면 외각에 2줄의 0을 만들어냄. 임의적으로 이미지 크기 늘려줌.
> stride = 컨벌루션 커널이 슬라이딩 하여 이동하는 정도, 크면 연산량이 줄어들고, output의 사이즈가 작아짐. 작으면 연산량이 증가하고 Output의 크기가 증가

> output height = (in_height - kernel height + padding * 2) // stride + 1
> output weight = (in_wieght - kernel weight + padding * 2) // stride + 1

> A * W = B라고 할 때,
> A shape \[batch, in_channel, in_height, in_weight]
> W shape \[out_channel, kernel_channel, kernel_height, kernel_weight]
> B shape \[batch, out_channel, out_height, out_weight]
> batch = 학습 할 때, 여러가지의 이미지 데이터를 한꺼번에 수행할 때 사용하는 파라메터

> 컨벌루션 연산량 (Convolution operation) - 슬라이딩 윈도우 컨벌루션
> MAC이라는 단어를 사용함. multiply accumulation operation
> convolution mac = kernel_weight * kernel_height * kernel_channal * out_channel * out_weight * out_height * batch
> kernel_weight * kernel_height * kernel_channal = 웨이트의 하나의 연산량 - 출력의 픽셀 1개의 연산량
> kernel_weight * kernel_height * kernel_channal * out_channel = 웨이트 전체의 연산 - 출력의 채널수만큼만의 연산량
> mac을 구하기 위해서는 7번의 루프가 필요함.

> 효율적인 방식으로 변환
> IM2COL & GEMM
> IM2COL = 다차원(디멘션)데이터을 2D 행렬로 변환시켜주는 것.
> 3차원 행렬을 2차원으로 변형시켜서 프로덕트하는 연산량을 줄임.
> GEMM = 두개의 입력 행렬을 곱해서 출력을 얻는 과정

> pooling = 입력 데이터에 대해서 커널의 해상도를 줄이는 것.
> 연산량을 줄이거나, 이 모델의 특징점을 요약해서 뽑아내고 싶을 때 사용함.
> max pooling = 커널 사이즈에 따라서 나눠진 픽셀들 중, Max에 해당하는 픽셀값을 출력하는 것.
> average pooling = 커널 사이즈에 따라서 나눠진 픽셀들의 평균에 해당하는 픽셀값을 출력하는 것.

> fully connected layer
> 컨벌루션 연산과 다르게 CNN에서 2D의 입력 데이터에서 지역정보를 가지고 있는 x y축을 1차원으로 변환시킴.
> 한 픽셀당 1 by 1으로 매칭 될 수 있게 동일한 숫자의 FC weight를 만들어서 dot 연산 후, 모두 더한 값을 출력하는 것.
> 어떤 레이어를 통해 2D로 나온 값을 1D로 변환시켜서 계산함.
> 컨벌루션 레이어에 비해서 해상도가 크다면 1 by 1으로 매칭해야하기 때문에, 연산량이 커진다는 단점이 있음.

> Activation = 활성함수
> 컨벌루션과 fully layer를 통해 나온 값을 유의미한 값을 두드러지게 활성화 시키고, 무의미한 부분은 음수의 값으로 표현하여 값의 차이를 주는 것.
> 비선형 함수임. = 딥러닝 모델에서 웨이트를 갱신할때 사용
> 미분값을 계산할 때, 각각의 x값에 따른 그래디언트 값이 조금씩 차이가 있기 때문에 이 값들을 유의미하게 웨이트를 갱신 할 수 있다.

![image](https://user-images.githubusercontent.com/55529455/164180803-9302db8e-9013-4801-be8a-1d920bc70f5f.png)

> Shallow CNN (얕은 CNN)

![image](https://user-images.githubusercontent.com/55529455/164188573-ceb0429f-7680-4f44-98db-de72b7bb4245.png)

> forward만 구현했다면, backward 또한 구현해볼 예정.
> forward를 통해 에러값을 비교할 수 있고, 해당 값을 미분하여 미분값에 대해 계산하게 하여 backward 구현 예정

> max pooling backpropagation의 특이점
> forward의 경우는, 커널에 의해 나눠진 값의 가장 큰 값을 이용하여 만든다
> backward는 뽑아온 위치가 1로 표시가 되고(기울기 값), 나머지는 0으로 표시가 됨.

> backward 풀이
> 우리가 공유한 네트워크는 2개의 웨이트로 분류됨

![image](https://user-images.githubusercontent.com/55529455/164196144-5e504eb7-7c8f-4cc6-9d17-c689e6af478f.png)
![image](https://user-images.githubusercontent.com/55529455/164196681-07819d3a-d026-44d7-8d3e-dce9e8507027.png)
![image](https://user-images.githubusercontent.com/55529455/164198813-c690af3f-4ccc-4835-8491-bae5867982ce.png)
![image](https://user-images.githubusercontent.com/55529455/164199031-dbe2f509-9b72-4a91-b03d-7f19b6519c9a.png)
![image](https://user-images.githubusercontent.com/55529455/164199231-b5269c74-bd91-4180-80aa-7b2413cdfbf2.png)
![image](https://user-images.githubusercontent.com/55529455/164199328-ba9b660b-1aff-4cb0-884f-227a14855e3d.png)






















