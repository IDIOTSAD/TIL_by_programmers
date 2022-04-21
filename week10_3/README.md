# 강의 요약

> Training model
> 한번씩 포워드하고, 백워드로 웨이트를 업데이트 하면서, 트레이닝 데이터에 맞게 피팅이 됨.
> 웨이트가 정교해지면서, 많은 데이터를 보게 되고, 학습데이터에 맞게 에러값(로스)이 줄어드는 과정
> 그레디언트 디센트 메소드(경사하강법)를 많이 사용함 - 각각의 로스 턴의 미분값 기반으로 한 것을 곱하여 기울기값으로 경사하강법으로 로스를 줄여나감

> Optimizer
> 최적화를 시키는 방법들 - 미분값을 구하고 업데이트 시켜주는 수식에 따라 많이 달라짐
> 로스값을 줄이기 위해 경사하강법으로 딥러닝이 수렴하는 것이 공통적인 개념

> 기존의 경사하강법
> 트레이닝값이 100장이 있으면 포워드를 통해서 각각 로스값을 구하고 각각 로스에 대해서 그레디언트의 미분값을 구해서 한번에 갱신하는 것
> 100개를 다 보고, 100개 데이터에서 나온 로스 값을 통해서 경사하강법 계산해서 하는 것 (100번을 한번 보고 모든 값들을 한번 봐서 웨이트 갱신하는 것)
> 몇번을 볼 동안 웨이트를 갱신못하는 단점이 있음 - 수렴이 어려움.

> SGD (Stochastic Gradient Descent)
> 100개를 한번에 보고 갱신하지 않음. - 각각 1개 데이터에 포워드, 백워드를 하고, 에러값을 가지고 웨이트의 경사하강법 계산을 하여 업데이트를 함.
> 더 많이 웨이트 갱신가능.
> W - W - eta (dL / dw)
> MGSD (mini-batch gradient descent) - 전체 데이터가 아니라, batch의 수만큼 포워드, 백워드에 대한 에러 값을 경사하강법을 구해 웨이트 갱신
> SGD - 한 장의 이미지만 보고 웨이트 갱신, MGSD - 여러장의 이미지를 보고 웨이트 갱신
> 이미지 한장당 갱신하면, 노이즈, 하드케이스 이미지 (생소한이미지) 웨이트에 부정적인 영향을 주는 데이터가 있다면 부정적으로 웨이트가 갱신됨
> 이를 위해서 MSGD가 나온것임. 여러장의 이미지를 한꺼번에 해서 웨이트를 갱신하기 때문에 아웃라이어 데이터도 어느정도 정규화가 됨

> Momentum
> velocity term 기반.
> 경사가 하강되는 방향을 하강하는 것을 의미함.
> v = alpha * v - eta(dl / dw)
> w = w + v
> 기존의 웨이트가 local minimal 에 빠지는 경향을 해소시켜줌. - global minimal로 가게 만들어줌 (속도가 있기 때문에)

> AdaGrad
> 가장 큰 미분값을 전부 더해주고, 제곱을 씌우고 루트를 하는 것
> 평균적인 값으로 학습을 진행하여 노이즈 같은 것에 강하게 만듬.
> 많이 느리다는 단점이 있음. 수렴이 잘 안됨.

> RMS-prop
> AdaGrad의 단점을 해결해서 나온 옵티마이저
> 수렴이 잘 안되는 부분을 해결하였음.

> Adam
> RMPS-prop + Momentum

![image](https://user-images.githubusercontent.com/55529455/164375572-75ad558b-73ed-4598-b3ba-1f1caffd3904.png)

> SGD가 Adam보다 좋은가?
> 유동적인 메소드 (Adam, RMPS-prop)은 비유동적인 메소드 (SGD, Momentum)보다 안좋다는 논문이 나오고 있음.

> 오버피팅
> 차트를 보았을 때, train loss set을 봤을 때는 내려갔더라도, test, eval loss set에서 loss가 증가하는 현상

> 언더피팅
> 모든 loss가 높을 때 의미함 - 학습이 덜 됐음을 의미

> Regularization
> 모델이 가지고 있는 웨이트가 큰값들을 가지고 있으면, 그 값들로 인해서 포워드 해서 결과가 나왔을 때, 오버피팅이 될 수 있음.
> 값들이 큰 웨이트들을 패널티를 부여하는 것.
> 오버피팅을 방지하기 위한 기법

> L1 Regularization
> 절대값을 써서 sum을 하고 람다를 곱해서 loss term에 더해지는 방식

> L2 Regularization
> 제곱에 루트를 씌워서 사용하는 방법 - 좀 더 스무스한 값으로 나오는 경향이 있음.

> 모델에 대해서 짜고 포워드 백워드를 하는데, 가끔씩 오버피팅 되는 원인 중 하나가 특정값에 바이어스가 될 수 있다.
> 값이 큰 경우에 해당함. - 이 경우는 Regularization을 사용하여 해결하였음.

> Drop out
> 각각의 웨이트들을 죽이는 것을 의미함. 랜덤한 웨이트를 죽여서 사용하지 않는 방법
> 오버피팅을 피할 수 있는 기법
> 학습할 때만 사용하고, inference에서는 사용하지 않음.

> batch normalization
> 일반적으로 컨벌루션을 하고, 배치노멀라이제이션 을 하고, Relu (activation)하는 방식에서 사용함.
> 컨벌루션과 activation사이에 사용함
> 컨벌루션을 통해 나온 값은 여러 range로 나오게 됨.
> 해당 기술이 없다면, 컨벌루션 결과가 음수가 많을 때 바로 활성함수를 하게 된다면, -부분은 0이 되기 때문에(Relu) 실제 학습 때, 일부 값만 들어가는 문제 발생
> 바이어스된 값을 가지면 안되고, 정규화된 값이 있어야 좀 더 정밀하게 나올 수 있다.
> 안정적인 분포의 값을 가지도록 만듬.
> 필수적인 요소 중 하나.


# object detection

> 이미지를 보고 분류하는 것 - Classification
> 객체가 하나의 object가 있을 때, 위치까지 알 수 있도록 정보 제공 - Object Localization
> 객체가 여러개 있을 때, 위치를 알려주는 정보 제공 - Object Detection

> 객체의 결과 값이 확률 분포로 나오게 됨. - Classification의 기본 결과 class_socre\[예측된 결과값, 각각의 object 클래스]
> Classification + \[x, y, w, h] 4개의 포인트 값이 추가가 됨. - Localization (바운딩 박스가 추가 됨.) 위의 배열에서 + 4개가 됨.

> 예전에 제안된 object detection
> 슬라이딩 윈도우를 써서 다중 객체 인식이 가능할 것이다. - 이미지 한장을 보는데도 많은 연산이 필요한데, 여러개를 찾으려면 inference하는데 자원이 많이 듦.
> 오브젝트가 큰지 작은지 알 수 없고, 가변적인 크기를 할 수 없었음.

> 요즘 많이 쓰이는 방식
> classification + regressor가 추가 됨. regressor = bounding box와 같은 정보를 담음

> Classification vs Object detection
> 마지막 레이어 쉐이프가 다름.
> Object detection은 위치 개념이 있기 때문에, 2D feaature로 표현을 해야함.
> Classification은 위치 개념이 없기 때문에 1D feature로도 표현이 가능.
> 일반적인 Classification = \[1, 1, class_num]
> 일반적인 object detection = \[H, W, class_num + box_offset + confidence] (1 스테이지)

> object detecion의 아키텍쳐
> stage의 개념 = 얼마나 forward를 하는지
> two-stage detection = 한번 forward하고, 예측된 결과 값을 또 forward하여 최종적으로 결과를 출력하는 것. (Faster-RCNN) - 정확하지만, one-stage보다 느림.
> one-stage detection = 한번에 forward해서 나온 예측값을 바로 결과로 내는 것. (SSD, YOLO) - 속도는 빠르지만, tow-stage보다 정교하지 않음.

> one stage object detector architecture
> backbone - lenet5, vgg 등 classification 모델 (Feature extractor)
> neck - backbone에서 뽑아낸 이미지(낮은 것 부터 큰 것까지)에서 단계적으로 각각 다른 해상도 값을 가지는 feature map을 병합하는 것. (feature pyramid)
> dense prediction - 각 feature map에서 학습되어 도출되는 object의 예측값에 바운딩 박스를 채워놓음.

> feature들이 backbone을 통해 추상화가 됨. 레이어가 깊어질수록 추상화가 심해짐.

> neck부분에서 feature들이 섞이고 더해지게 되는데, 작은 해상도를 가지는 feature를 업스케일링을 통해 해상도를 갖게 한다. (H, W가 동일해야함.)
> 만든 feature가 채널이 다른 경우 뒷단 채널에 붙이는 것을 concat이라 함. \[2C, H, W]가 되는 것임.
> 채널수까지 똑같은 경우, 더해서 1개의 새로운 feature를 만드는 것을 add라고 한다. \[C, H, W]가 되는 것임.

> dense Prediction의 경우, 클래스에 대한 정보를 담는 개수, 확률값을 담은 값, 바운딩 박스 값을 가지는 결과 값을 header라고 함.

> two stage object detector architecture
> 1번째 포워드에서는 피쳐맵이 나올 때, 오브젝트가 맞다고 예측하는 부분에 proposal 하고, 위치에 대한 학습이 진행됨.
> 그리고, path에 대한 정보를 입력을 넣어서 다시 오브젝트 위치에 대한 분류와 바운딩 박스를 함.
> 1번째 포워드는 후보들을 뽑는 과정이 되고, 2번째 포워드에서는 후보 영역중 inference를 통해 실제 object를 확인하는 과정.

> one stage까지 진행하는 것은 동일. 이후에 1개가 추가가 됨. sparse prediction.
> 후보 영역들을 다시 한번 분류, 바운딩 박스 작업 수행.

> grid - 피쳐 맵의 픽셀 수를 grid라고 함.
> 격자로 object를 찾아내는 것.












