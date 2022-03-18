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






