# 1장 요약 (영상 불러와서 출력하기)

> * 소스코드

![image](https://user-images.githubusercontent.com/55529455/158304319-cca903ff-576f-4aa2-82eb-64b646273776.png)

> * #include "opencv2/opencv.hpp" 하나만 선언 해줘도 나머지 다른 hpp가 선언이 됨.
> * using namespace는 코드를 간결하게 하기 위해서 사용함. std::cout 등을 cout으로만 실행되도록 만들 수 있음.
> * imread = image read
> * Mat = 행렬 데이터 (이미지를 행렬 데이터로 저장함)
> * imread가 제대로 불러오지 못하면 (경로 문제), img에 제대로 값이 들어가지 않음
> * namedWindow = 이미지 창을 엶.
> * imshow = image show
> * waitKey() = 사용자의 키를 기다림 - 키를 누르면 다음 코드를 동작하게 됨.

> * OpenCV 주요 함수

![image](https://user-images.githubusercontent.com/55529455/158310290-04b3a52d-76d0-425e-99c5-58a48b40e4f6.png)

![image](https://user-images.githubusercontent.com/55529455/158310541-c8fcffa2-b5ca-4897-a146-78ea24384fc1.png)

![image](https://user-images.githubusercontent.com/55529455/158310633-42577f48-1773-4fe4-99b0-dd9c0b4d3c80.png)

![image](https://user-images.githubusercontent.com/55529455/158310817-1ffbcc1b-0c7a-4622-b604-777bb0575022.png)

![image](https://user-images.githubusercontent.com/55529455/158310853-64192318-6f80-49a9-8ed3-2f7ca8f57df8.png)

![image](https://user-images.githubusercontent.com/55529455/158310887-e4486b0c-4ab7-46fd-ad09-b993766d12f5.png)


