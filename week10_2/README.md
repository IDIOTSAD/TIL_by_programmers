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





























