# 강의 요약

> * 히스토그램 스트레칭
> * 영상의 히스토그램이 그레이스케일 전 구간에서 걸쳐 나타나도록 변경하는 선형 변환 기법
> * 특정 구간에 집중되어 나타난 히스토그램을 마치 고무줄을 늘리듯이 펼쳐서 그레이스케일 범위 전 구간에서 히스토그램이 골고루 나타나도록 변환
> * 즉, 히스토그램을 늘려서 흰색과 검정색이 있도록 표현 (Gmin 이 0으로 가고, Gmax가 255로 감, 최대 범위가 Gmin ~ Gmax로)

> * 히스토그램 스트레칭 변환 함수 - 변환 함수의 직선의 방정식을 구하기
> * 기울기는 255 / (Gmax - Gmin)이 됨.
> * Gmin : Gmax - Gmin = x : 255
> * y절편 = (-255 * Gmin) / (Gmax - Gmin)

![image](https://user-images.githubusercontent.com/55529455/158936671-3b20c3f0-9066-4cc3-9217-ceab9da97563.png)
> * minMaLoc를 이용하여 히스토그램의 Gmin, Gmax를 구한다. => 파라메터 구성 - (영상, &min, &max)
> * 혹흔, normalize 함수를 이용해서 minMaxLoc 이후, 위의 식을 계산해주는 것과 똑같음. => 파라메터 구성 - (입, 출, 최소, 최대, NORM_MINMAX)

> * 히스토그램 평활화
> * 히스토그램이 그레이스케일 전체 구간에서 균일한 분포로 나타나도록 변경하는 명암비 향상 기법
> * 히스토그램 균등화, 균일화, 평탄화

> * 히스토그램 평활화를 위한 변환 함수 구하기

![image](https://user-images.githubusercontent.com/55529455/158938137-bb207d7e-b88a-4d13-84b9-4a422e95579f.png)
![image](https://user-images.githubusercontent.com/55529455/158938563-3fd37ec4-1cde-4c91-b0d5-cbf119b76be8.png)
![image](https://user-images.githubusercontent.com/55529455/158938965-157b673e-3e64-4076-abb6-1c364e108caa.png)

> * 픽셀값이 뭉쳐있으면 펴고, 안뭉쳐있으면 그대로 두는 것이, 히스토그램 평활화.
> * 스트레칭은 선형으로 히스토그램을 적절하게 펼치고, 평활화는 히스토그램 전 구간에서 균일하게 나오게 상대적으로 많이 펼침.

> * 가중치의 합, 가중치의 곱 - 기존에 배웠던 saturate 값에 대해서 각각의 영상에 합하거나 곱하는 것. (saturate 하는 이유는 보정하기 위해서)
> * dst(x,y) = saturate(scr1(x,y) +(\*) src2(x,y))
> * 평균 연산의 응용 - 잡음 제거

![image](https://user-images.githubusercontent.com/55529455/158941466-1789bfe8-4e52-40b2-b809-d4cc29e60a69.png)
> * 고스트 연산 = 어둡게 여러번 찍어서 합성시킴.

> * 뺄셈 연산
> * dst(x,y) = saturate(scr1(x,y) - src2(x,y))

> * 차이 연산
> * dst(x,y) = saturate(|scr1(x,y) - src2(x,y)|)

![image](https://user-images.githubusercontent.com/55529455/158942039-903bda11-209d-4f3a-a297-dd0ea15eb0ee.png)
![image](https://user-images.githubusercontent.com/55529455/158942274-14dd45b9-5dfb-4d0c-afe4-d86c023ce68a.png)
![image](https://user-images.githubusercontent.com/55529455/158942074-fadf7797-5c24-485a-ba28-00cad82a4297.png)
![image](https://user-images.githubusercontent.com/55529455/158942229-745d8c95-442a-4c98-8d7e-8d9200ea3b20.png)

> * 필터링
> * 영상에서 필요한 정보만 통과시키고, 원치 않는 정보는 걸러내는 작업

> * 주파수 공간에서의 필터링
> * 푸리에 변환을 이용하여 영상을 주파수 공간으로 변환하여 필터링을 수행하는 방법 (로우패스필터, 하이패스필터 등을 사용)
> * 공간적 필터링
> * 영상의 픽셀 값을 직접 이용하는 필터링 방법 - 대상 좌표의 픽실겞과 주변 픽셀 값을 동시에 사용
> * 주로 마스크 연산을 이용함 (마스크 ~ 커널) (3x3, 5x5, 7x7)
> * OpenCV에서는 공간적 필터링 마스크 크기가 커질 경우, 주파수 공간에서의 필터링을 수행함.

> * 다양한 모양과 크기의 마스크
> * 필터링에 사용되는 마스크는 다양한 크기, 모양을 지정할 수 있지만, 대부분 3x3 정방향 필터를 사용 - 마스크는 보통 홀수로 사용함.
> * 마스크의 형태와 값에 따라 필터의 역할이 결정됨
> * 영상을 부드럽게, 날카롭게, 엣지검출, 잡음 제거 등

![image](https://user-images.githubusercontent.com/55529455/158947110-5752b95c-2aa2-4bf9-b7be-ba9dc0e055e6.png)
> * 여기서 수행하는 연산을 Correlation (Convolution)이라고 함.

![image](https://user-images.githubusercontent.com/55529455/158948233-c80d8447-73a6-4992-ad8c-88cb828e2b48.png)
![image](https://user-images.githubusercontent.com/55529455/158948456-708ab830-ec32-4f69-a88f-dc68e6f5a308.png)
![image](https://user-images.githubusercontent.com/55529455/158948769-a7068faf-ac8e-4d8e-adbf-5e94c7094373.png)
![image](https://user-images.githubusercontent.com/55529455/158949151-cc3e9bb0-9224-429b-8d1f-40c62411215f.png)

> * 엠보싱
> * 직물이나 종이, 금속판 등에 올록볼록한 형태로 만든 객체의 윤곽 또는 무늬
> * 엠보싱 필터
> * 엠보싱 필터는 입력 영상을 엠보싱 느낌이 나도록 변환하는 필터
> * 결과를 효과적으로 보여주기 위해 결과 영상에 128을 더해서 보여줌.

![image](https://user-images.githubusercontent.com/55529455/158949330-455ab615-8ce2-4baa-a7be-3b999870162f.png)

> * 평균값 필터
> * 영상의 특정 좌표 값을 주변 픽셀 값들의 산술 평균으로 설정
> * 픽셀들 간의 그레이 스케일 값 변화가 줄어들어 날카로운 엣지가 무뎌지고, 영상에 있는 잡음의 영향이 사라지는 효과
> * 3x3은 1/9, 5x5는 1/25가 됨.

![image](https://user-images.githubusercontent.com/55529455/158951055-356027b0-2d70-4645-b1e8-8dd00563b2e9.png)





