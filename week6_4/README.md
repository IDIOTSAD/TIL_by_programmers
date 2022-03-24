# 강의 요약

> * 특정 색상 영역 추출
> * RGB, HSV, YCrCb등의 색 공간에서 각 색상 성분의 범위를 지정하여 특정 색상 성분만 추출

![image](https://user-images.githubusercontent.com/55529455/159840634-d58b3b19-18ee-4762-9a65-69f792fea696.png)
> * H와 S 부분으로 계산하여 출력 하면 됨. (색상, 채도)
> * RGB에서 계산해도 되긴 함. = 하지만, 잘 될때도 있지만, 영상에 변화가 생기면, 다른 표현에 비해서 추출이 힘듬.
> * 즉, HSV가 음영 부분에 강하다고 볼 수 있음. = 변화에 민감하지 않음.
> * 위 사진의 두가지 사진을 합성 시키면, 원하는 색상만 보이게 할 수 있음.

![image](https://user-images.githubusercontent.com/55529455/159840863-928d397c-80d6-4b30-b0cd-4787bcd11c14.png)
> * lowerb ~ upperb 에 만족하면 흰색, 아니면 검정색 출력

> * 히스토그램 역투영
> * 주어진 히스토그램 모델에 영상의 픽셀들이 얼마나 일치하는지를 검사하는 방법
> * 임의의 색상 영역을 검출할 때 효과적
> * 해당 히스토그램에 대해서 일치하는 색상을 찾는 것임. - 픽셀 값 분포에 가우시안을 하는 경우도 있음. ( 좀 더 부드러운 히스토그램 이용)
> * BGR에서 YCrCb로 변환하고, Y는 무시하고 Cr과 Cb 값으로 점을 찍어서 보게 되면, 밝은 회색으로 보이게 됨.
> * 이걸 이용해서, 전체 픽셀에 대해서 히스토그램에 부합되는 픽셀을 하나하나 찾아서 밝은 회색으로 변화 시켜서 마스크화 하고, 영상을 합성시킴.

![image](https://user-images.githubusercontent.com/55529455/159843660-f3ee7a2c-ae9a-4e73-a2ee-d06e19ba5b6c.png)

> * 에지
> * 영상에서 픽셀의 밝기 값이 급격하게 변하는 부분
> * 일반적으로 배경과 객체, 또는 객체와 객체의 경계

> * 기본적인 에지 검출 방법
> * 영상을 (x,y) 변수의 함수로 간주했을 때, 이 함수의 1차 미분(순간변화량) 값이 크게 나타나는 부분을 검출함.

> * 가우시안 블러와 에지 검출
> * 입력 영상에 가우시안 블러를 적용하여 잡음을 제거한 후 에지를 검출하는 것이 바람직함.

![image](https://user-images.githubusercontent.com/55529455/159849295-c75a894e-ee5f-4905-82b9-8900a894e069.png)
![image](https://user-images.githubusercontent.com/55529455/159849711-e0159981-930a-4642-9dfe-13494957e1d2.png)
![image](https://user-images.githubusercontent.com/55529455/159849987-3514d88e-457b-445c-9f76-91614ef4a3f3.png)
![image](https://user-images.githubusercontent.com/55529455/159850074-4de95c20-ee9a-48ac-8596-7e38feeee6b1.png)
![image](https://user-images.githubusercontent.com/55529455/159854014-4f93422b-e509-4ebb-9578-b1f9d1313aa2.png)
![image](https://user-images.githubusercontent.com/55529455/159853991-57b1a882-eaf6-44fc-9849-ecb68e765e9f.png)
![image](https://user-images.githubusercontent.com/55529455/159855194-ecba8725-b654-4f01-a5ec-ebb6150594cc.png)
![image](https://user-images.githubusercontent.com/55529455/159855642-17739119-dd83-4617-8971-909484ebcdaa.png)

> * 케니 에지 검출기
> * 좋은 에지 검출기의 조건 = 케니 에지 검출기의 특징
> * 정확한 검출 = 에지가 아닌 점을 에지로 찾거나 또는 에지를 검출하지 못하는 확률을 치소화
> * 정확한 위치 = 실제 에지의 중심을 검출
> * 단일 에지 = 하나의 에지는 하나의 점으로 표현

![image](https://user-images.githubusercontent.com/55529455/159856665-c198a483-7885-41e1-8aa4-8df8e91fe542.png)
> * 그레디언트 계산 = 픽셀값이 순간적으로 증가하는 크기와 방향을 추출. ex) 바둑판 모양
> * 비최대 억제 = 하나의 에지가 여러개의 픽셀로 표현되는 현상을 없애기 위해서 그래디언트 크기가 국지적 최대인 픽셀만 에지 픽셀로 설정
> * 그래디언트 방향에 위치한 두 개의 픽셀과 국지적 최대를 검사함.
> * 가운데 있는 흰색 부분만 엣지로 추출함. (245 기준으로 봤을 때, 135의 경우 그 바로 옆에 있는 12와 비교하였을때 크기 때문에 무시함.)

> * 히스테리리스 에지 트래킹
> * 두개의 임계값을 사용 (Tlow, Thigh)
> * 강한 에지 = ||f|| >= Thigh = 최종 에지로 설정
> * 약한 에지 = Tlow <= ||f|| < Thigh = 강한 에지와 연결된 픽셀만 최종 에지로 설정.
> * Tlow 보다 작으면 무조건 에지가 아니고, Thigh 보다 높으면 무조건 에지, Thight과 연결되어 있지만, Tlow보다 큰 에지는 에지라고 판단함.

![image](https://user-images.githubusercontent.com/55529455/159858194-c46bc683-55fa-4737-96d8-0f9f8c6216da.png)
![image](https://user-images.githubusercontent.com/55529455/159858983-82cd0abe-d45e-4b08-ac3b-9750326c5e8b.png)



