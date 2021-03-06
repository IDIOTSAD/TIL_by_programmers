# 강의 요약

> one-stage object detection
> yolo : you look only once
> yolo backbone - googlenet(yolo v1), darknet19, darknet53

> ssd : single shot detection
> backbone - vgg16

> two-stage object detection
> RCNN
> selective search를 이용해 2000개의 후보를 뽑음. - 연산량 증가
> 2000개 뽑은 거에서 227 * 277로 리사이즈
> 이후, bounding box regression을 수행하고, 클래스를 SVM 분류를 수행하였음
> 연산량이 너무 많음. 성능은 좋음.

> Fast -RCNN
> 입력 데이터가 들어가면 CNN모델을 통해서 후보를 뽑음.
> ROI pooling을 사용하여 resize하지 않음. - 내가 원하는 feature map size로 pooling하는 것
> resize의 간섭사항을 해결함.
> SVM 분류기를 사용하지 않고, softmax regression을 사용함.
> 빨라졌지만 느림

> Faster - RCNN
> RPN을 하고, selective search 사용하지 않음.
> proposal을 뽑으면, 풀리 커넥티드 레이어를 통해서 분류와 바운드 박스 종류의 데이터를 얻음.
> 후보군을 보고 해당 부분을 다시 학습하기 때문에, 1스테이지에서 어느정도 오브젝트를 판단하고, 2스테이지에서 바운딩박스, 클래스 정보를 다시 한번 더 레이어를 수행
> 후보군 피쳐맵에 대해서 클래스, 바운드박스 정보를 위해 웨이트가 또 갱신되기 때문에, 1스테이지 디텍션보다 성능은 좋음.

> Precision (정밀도)
> 내가 예측한 총 바운딩 박스 중에서 진짜로 인식한 것들을 의미
> 20장 사진 중, 100개를 예측함, 80개는 맞추고 20개는 틀렸을 때, TP는 80, FP는 20
> 정밀도 계산 = 80 / (80 + 20) = 0.8 ( tp / (tp + fp))

> Recall (재현율)
> 분모가 전체 gt. gt값 중에서 내가 검출한 값들. 내가 정말로 맞춘 비율 (정답 중에서 내가 맞춘 비율)
> 20장 사진 중, 100개를 예측 했는데, 80개 바운드 박스는 맞추고 20개는 틀렸을 때, GT는 130, TP는 80, FP는 20개 FN은 50
> 재현율은 80 / (80 + 50) = 0.533 ( tp / (tp + fn))

> F1 score
> 정밀도와 재현율의 조화평균
> 2 * ((정밀도 * 재현율) / (정밀도 + 재현율))
> 높은 정밀도, 높은 재현율 - 완벽한 모델
> 낮은 재현율, 높은 정밀도 - 바운딩 박스 예측을 잘 못한 경우, 바운딩 박스의 값이 신뢰가 없음.
> 높은 재현율, 낮은 정밀도 - 바운딩 박스 검출은 잘했는데, 다른 클래스 검출이 많은 경우
> 낮은 재현율, 낮은 정밀도 - 부족한 모델

> TP = 옳은 검출, FP = 틀린 검출, FN = 검출되야하는데 안된 경우, TN = 검출되지 않아야 하는 부분에서 검출된 부분

> PR curve
> 정밀도와 예측값의 그래프 x 축은 재현율, y축은 정밀도
> 예측한 Prediction의 값들에서 검출된 클래스 확률이 나올 것이고, sorting 해서 상위부터 나열 함.
> TP, FP의 값에 대한 각각의 값에 누적을 하는 방법을 사용. 이렇게 해서 재현율과 정밀도를 구함.
> PR curve가 1에 가까이 가는 것이 best 모델
> PR curve의 적분한 값의 시그마로 mean average precision (mAP)를 구하게 됨.

> confusion matrix
> TP와 FP가 클래스간의 얼마나 등장했는지 카운팅해서 표로 표현한 것.
> 어디서 FP가 많이 뜨는지에 대해서 알 수 있음.

***

> 논문 쉽게 읽는 방법
> abstrack을 보면, 전체적인 내용을 볼 수 있다.
> Conclusion은 결과를 나타내는 것.
> figure을 보는 방법

> abstrack
> 기존의 object detection은 classifiers와 연동된 내용이 많았음.
> 본인들이 낸 yolo는 바운딩 박스와 클래스 항목으로 풀어 내었다.
> 싱글 뉴럴 네트워크를 사용해서 바운딩 박스와 클래스를 예측하였고(한번에 forward로 전체 이미지에서) 평가하였음.
> 싱글 네트워크고, 성능을 끌어올리는데 최적화 되어있음.
> 초당 45프레임이므로 실시간이다.

> conclusion
> unified model에 충족 하였음.
> 단순하면서, 전체 이미지를 직접적으로 학습하는 방식을 이용함.
> 분류 베이스 방식이 아니라, 전체 모델의 검출 성능을 연결되게 해놨음.
> 가장 빠른 객체 인식 모델이다.
> fast r-cnn에 비해서 인식은 안좋아도, background 점유율이 낮음.

> introducion
> 객체 인식에서 자율주행에 사용하기 위해서는 실시간으로 인식하기 위한 장치가 필요하다.
> 현재 검출 시스템은 분류 기준으로 하고 있다. - 그런 방식은 슬라이딩 윈도우 접근법을 사용함.
> R-CNN 방식을 사용하기도 한다 - 바운딩 박스를 뽑아내고, 바운딩 박스에서 분류를 사용하기 때문에 느리다. 모델도 크다.
> single regression 방식인 yolo를 소개함.
> 448 * 448 방식으로 검출을 수행한다.
> yolo는 빠르다 - 컴플렉스 파이프라인이 필요 없음. 1초에 45 픽셀을 검출함. (titan x 기준)
> yolo는 다른 실시간 객체검출 시스템에 비해 2배 빠름
> yolo는 학습 할 때, 전체 이미지를 봄. - 피쳐 이미지에 대한 정보를 각각의 클래스의 정보로 한꺼번에 보게 됨.
> yolo는 일반적인 객체의 특징을 학습하는 점을 가짐. - 빠르게 각각 분류하고, 위치를 알아내는 특징

> unified detection
> 전체 이미지에서 각각의 객체에 대한 정보를 뽑아내는 방식
> end to end (처음부터 끝까지) 학습하는 방식
> S x S 입력이미지를 grid 방식으로 분류하게 됨.
> center에 객체가 grid cell 안에 들어올 때, 그 객체를 담당하는 셀로 변경하게 됨.
> 각각의 그리드 셀은 B 바운딩 박스를 찾고, 컨피던스 코어를 찾게 됨.
> 컨피던스 코어는 실제로 객체가 얼마나 있는지에 대한 정보임. 객체 확률값 * IOU
> 객체가 셀에 없을 때는 confidence를 0으로 둠.
> 바운딩 박스의 구조는 x, y, w, h, confidence로 구성됨.
> x, y, w, h, pro, pr0, .. prn(클래스의 개수) - 5개의 바운딩 박스 구조와 클래스의 개수로 구성됨.
> S x S x (B * 5 + C) - 각각의 확률값 * IOU ex) S = 7, B = 2이고, 20개의 클래스가 있을 때, (C = 20) = 7 * 7 * 30

> network design
> googlelenet을 사용함.
> 24개의 컨벌루션 레이어
> 2 fully connected layer
> fast yolo는 9개의 컨벌루션 레이어 약간의 필터로 구성됨.
> input 해상도 = 448 * 448, 컨벌루션이 진행되고, 마지막으로 FC가 붙어있는 식
> imageNet 88% 달성
> 활성함수로 leakyrelu를 사용함. - relu에서 약간 다름.
> relu는 음수는 0, 양수는 그레디언트 diff 1값.
> leakyrelu는 음수에서 약간의 그레디언트를 부여. (0.1x)
> 분류에러랑 동일하지 않기 때문에 weight를 부여하였음.
> 람다 코디네이터와 람다눕제이로 하이퍼파라메터를 부여함. (코디네이터 - 물체가 있다고 판단한 값, 눕제이 - 물체가 없다고 판단한 값)
> MSE 방식의 loss를 사용하였음.
> low recall - 재현율이 낮았다. - 실제 객체를 잘 찾지 못했음.
> box regression - 바운딩 박스 위치가 안좋았음.

***
> yolo 9000, yolo v2에 관한 논문

> abstrack
> v2는 v1에 비해서 fps, map등이 많이 상승하였음.
> 조인트 트레이닝이라고 해서, 레이블되지 않은 데이터를 사용 하였음.

> conclusion
> v2는 빠르고, 다양한 이미지 사이즈로 학습 해서 다양한 이미지 사이즈를 가지고 inference 할 수 있음.
> 이미지 사이즈가 작으면, 속도가 올라감. (연산속도 관련)
> wordTree 방식으로 사용해서 9000개 객체를 분류 할 수 있었음.

> Introduction
> imageNet을 사용하였음.
> yolo v1은 localization error와 low recall 에러가 많았음.
> batch normalization을 하였음. - 컨벌루션 레이어가 있으면, 배치 레이어를 추가함. 그리고 활성함수를 추가하는 방식을 사용함.
> 기존의 dropout 방식을 사용하지 않게 됨. mAP가 2% 상승하였음.
> High Resolution Classifier를 사용하였음. - 기존 v1은 224 x 224를 사용하였지만, v2에서는 448 x 448로 학습하였고, 4%의 mAP 상승이 있었음.
> 앵커박스를 사용하였다. FC를 삭제하였음. - FC는 컨벌루션의 공간정보를 1차원으로 축소시키기 때문에 차원 정보가 사라지는 단점이 있었음. (FC는 Fully connectied layer)
> 따라서, 448 x 448 -> 13 x 13 를 그리드로 사용하는 방식으로 하였음.
> 98개의 박스를 각각의 이미지에서 찾는데(앵커박스 사용) mAP는 약간 감소하였지만, 7%의 recall 성능 향상이 되었음.
> Dimension Clusters를 사용하였음. - v1에서는 박스 디멘젼이 정해져 있음. 7 x 7 그리드로 나오기 때문에, 영역안에서 찾아야하는 단점을 해결하였음.
> k-means를 사용하여 앵커 사이즈를 조절해줌. (k-means는 주어진 데이터를 k개의 클러스터로 묶음, 각 클러스터와 거리 차이의 분산을 최소화 함) - 객체가 가까이 군집함
> Direct location prediction을 사용함 - yolo v1에 앵커박스를 사용하여 불완전성이 있었음.(학습 초기 - x, y 코디네이터 찾는데 불완전성이 있었음.)
> 왜냐하면, x,y 값을 7 x 7에서 찾다보니 에러값이 큼 - gt와 거리차이를 MSE로 계산되다 보니 distance 차이가 많이 나면 loss값이 커짐. (초반 loss가 크면 학습이 잘 안됨.)
> 그리드 앵커에 대한 center 값을 빼줌으로써 각 센터의 기준으로 좌표에 맞게 값을 정규화 하였음.
> 네트워크 예측값은 5개의 바운딩 박스를 cell로 계산함. - tx, ty, tw, th, to로 구성됨 -> 그것을 계산함. 5%의 앵커박스 정확도가 올라감.
> 13 x 13으로 하다보니 좀 더 정확하게 객체를 찾을 수 있게 됨.

![image](https://user-images.githubusercontent.com/55529455/165100942-8598e5b9-f936-4650-aded-0ad51ee53a91.png)
> 실제로, resolution의 값을 유동적으로 할 수 있기 때문에, 해상도가 낮으면 fps가 증가, 높으면 mAP가 증가하므로 적절한 값을 찾아서 쓰면 됨.

> Darknet-19 backbone
> VGG 모델과 유사하지만, 3x3 필터를 사용함. batch norm도 사용, 잘 수렴할 수 있게 사용함. 19개의 컨벌루션 레이어와 5개의 maxpooling 레이어 사용.

***

> yolo v3 논문
> 320 x 320 사용함. v2와 유사함.
> 한개의 그리드에서 v2 까지는 multiple하게 했다면, 1개의 그리드에 1개의 바운딩 박스만 찾게 설계됨.
> N * N ( 3 * ( 4 + 1 + 80))의 구성으로 되어있음. 각각의 그리드안에 앵커가 3개를 만들어놔서 앵커 1개당 바운딩 박스가 (예측된) 하나씩 매칭되게 됨.
> 해당 부분에 박스정보, 객체 정보, 클래스 정보가 들어가 있는 방식.
> Darknet-53 사용 - 53개의 컨벌루션 레이어
> v2와의 차이점으로는 백본 이후, 3개의 레이어에서 예측한 바운딩박스를 각각 분리해서 3개의 피쳐맵에서 바운딩 박스를 예측함.
> 초반, 중반, 끝단에서 예측하기 때문에, grid의 size가 달라지는 경우의 장단점을 이용함. grid가 클수록 더 작은 객체를 찾기 쉬움. 작을수록 더 큰 객체를 찾기 쉬움.
> 앞단에서의 feature map을 섞어줌으로써 뒷단에 가져갈 수 있도록 해주는 시스템 - feature pyramid



