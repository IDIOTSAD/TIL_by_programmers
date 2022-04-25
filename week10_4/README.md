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



















