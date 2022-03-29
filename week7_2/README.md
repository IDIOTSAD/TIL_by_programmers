# 강의 요약

> * Warping
> * 사전적으로 뒤틀림, 왜곡하다라는 의미
> * 영상 시스템에서 말하는 Warping은 영상을 이동, 회전, 크기변환 등을 이용
> * 이미지를 찌그러뜨리거나 반대로 찌그러진 이미지를 복원하기 위한 처리 기법

> * 변환
> * 좌표 x를 새로운 좌표 x로 변환하는 함수
> * 사이즈 변경(Scaling), 위치변경(Translation), 회전 (Rocation) 등
> * 강제변환 (Rigid-Body) : 크기 및 각도가 보존되는 변환 (Translation, Rotation)
> * 유사변환 (Similarity) : 크기는 변하고 각도는 보존되는 변환 (Scaling)
> * Affine : 선형 변환과 이동변환까지 포함. 선의 수평선은 유지 (사각형 -> 평행사변형)
> * Perspective : Affine 변환에 수평ㅅ어도 유지되지 않음 (원근 변환)

![image](https://user-images.githubusercontent.com/55529455/160551490-2ebce225-5f2f-4bf6-bba3-7cf310c5ec42.png)
![image](https://user-images.githubusercontent.com/55529455/160551519-eb819791-008d-4aca-b21b-cf4acb88f43e.png)
![image](https://user-images.githubusercontent.com/55529455/160551560-6b15ee2d-5603-4bc3-a283-19a319f43e7d.png)
![image](https://user-images.githubusercontent.com/55529455/160551593-2df7f9b4-4dbc-4b56-8b9b-2b2772d971a2.png)
![image](https://user-images.githubusercontent.com/55529455/160551632-c550ed1f-6a76-4a1f-850c-5956be3d47c2.png)
![image](https://user-images.githubusercontent.com/55529455/160551698-4f34d332-9ea0-45a9-9ed4-d87ce1bb14d2.png)
![image](https://user-images.githubusercontent.com/55529455/160551722-b0919fef-b5ca-4c3f-a6a1-e110f160bc5c.png)
![image](https://user-images.githubusercontent.com/55529455/160551766-0c56a8c3-bd9d-409c-8370-7f66c4ac9070.png)
![image](https://user-images.githubusercontent.com/55529455/160551809-14ed54ea-a8ac-4307-ac3c-362a21658735.png)
![image](https://user-images.githubusercontent.com/55529455/160551854-28a1f743-4d51-413a-a039-48b6caa8aa49.png)
![image](https://user-images.githubusercontent.com/55529455/160551914-cbf8c1a3-6783-49db-ac26-403f255fbbc5.png)

> * 차선 검출에 Warping을 사용
> * 3차원 공간 - 원근현상 (먼곳에 있는 물체는 작게 보임)
> * Perspective 변환 적용
> * 하늘에서 보는 Bird Eye View -> 차선 찾기가 수월, 차선은 직선이기 때문에

> * Warping 과정을 거쳐서 차선 추출
> * 도로 이미지를 Bird Eye View 변형 처리 (Perspective 변환)
> * 차선을 찾아 그걸 다시 원본 이미지에 오버레이 함.

> * 원근 변환 - Perspective
> * 원근법을 적용한 변환
> * 직선의 성질만 유지되고, 선의 평행성은 유지가 안되는 변환
> * 기차길은 서로 평행하지만, 3차원에서 원근 현상으로 평행성이 유지못하고 하나의 점에서 만나는 것으로 보임.
> * 원근 현상을 없애는 변환이 가능함 - 차선 추출에 사용함 (4개의 점을 가지고 변환 행렬을 만들어서 사용한다.)
> * cv2.getPersepctiveTransform 함수를 통해 얻을 수 있음.
> * 이동할 4개의 점의 좌표가 필요 (어디서 어디로 변환할지 알려주는)
> * 결과값은 3x3 행렬임.

![image](https://user-images.githubusercontent.com/55529455/160555200-f0a5d0d0-f676-40e3-a688-0e753efeccbb.png)

> * 원근 변환과 슬라이딩 윈도우를 이용한 차선 찾기
> * Camera Calibration
> * Bird's Eye View
> * 이미지 임계값 및 이진 이미지
> * 슬라이딩 윈도우로 차선 위치 파악
> * 파악된 차선 위치 원본 이미지에 표시

> * 카메라 캘리브레이션 = 카메라 보정
> * 카메라는 곡면 렌즈를 사용해서 이미지를 형성 - 이로 인해 가장자리가 왜곡되어 보임
> * 가장자리가 왜곡됨으로 인해 물체의 크기, 모양이 변하게 되고, 시야의 위치에 따라 모양이 변하고, 실제보다 더 가깝거나 멀리 보임.
> * 이미지의 왜곡은 카메라의 다양한 내부적 요인들로 인해 발생
> * 렌즈, 렌즈-이미지 센서와의 거리, 렌즈와 이미지 센서가 이루는 각도 등
> * 이론 왜곡을 없애서 실제 우리 눈에 보이는 것과 같이 보정하는 것 = Camera Calibration
> * 왜곡된 지점을 왜곡되지 않은 지점으로 Mapping 하여 왜곡을 없앰.

> * 카메라 캘리브레이션을 위해서 체스판 이미지를 사용
> * 체스판 이미지는 규칙적이고 대비와 패턴이 강하기 때문에 에러 감지에 용이함.

![image](https://user-images.githubusercontent.com/55529455/160556203-dd2a08ca-9a6c-412f-99e6-846b0e105cd3.png)

> * Bird's-eye-View
> * 새가 하늘에서 내려다보는 듯한 구도로 위에서 아래로 내려다 보는 방식
> * 선의 곡률을 측정하기 위해서 도로 이미지를 하향식 보기로 변환 - 버드 아이즈 뷰
> * 1. 원근 변환 행렬 M을 계산하기 위해 소스 및 대상 지점이 주어지면 cv2.getPerspectiveTransform(src, dst)를 사용
> * -> cv2.getPerspectiveTransform(src, dst) = 원근 변환 행렬을 구하는 함수로, 4개의 점의 이동 전과 이동 후 좌표를 입력하면 이동 전 좌표로 이동후, 좌표로 투시 변환함.
> * 2. 역 원근 변환 계산을 위해서 cv2.getPerspectiveTransform(src, dst) 사용 = 앞의 원근 변환에서 src와 dst 값의 위치를 뒤바꿈
> * 3. 마지막으로 원근변환을 사용하여 이미지를 뒤틂.
> * -> cv2.warpPerspective(img, M, img_size, flags=cv2.INTER_LINEAR) = 앞서 계산한 원근 변환을 사용해서 이미지를 뒤틀어 원하는 구도로 변환

> * 원근 변환을 위한 4개의 점은 어디서 식별하는가?
> * 위에서 도로를 내려다 볼때, 직사각형을 나타내는 사다리꼴 모양의 4개의 점을 선택 (도로가 평면이라는 가정)
> * 가장자리 또는 모서리 감지를 통해 이미지에서 4개의 점을 감지하고, 색상 및 속성을 분석해 선택
> * 선택한 4개의 점을 적절하게 정렬 = 정렬이 올바르게 되지 않을 시 이미지가 엉켜서 출력됨.

> * 최종 사다리꼴 비율 및 차량 후드 자르기
> * bottom_width = 0.4, top_width = 0.0092, height = 0.4, car_hood = 45 (자동차 후드 제거를 위해 하단에 잘라낼 픽셀 수)
> * 하지만, 값은 유동적으로 변화 해야함.

> * 이미지 임계값, 이진 이미지
> * 차선이 명확하게 보이는 이미지를 생성하기 위해서 색상 임계값 조절
> * 이미지를 흰색과 노란색으로 마스킹
> * GrayScaling 수행
> * 이진 이미지 생성

> * HSV (H = 색조, S = 채도, V = 명도)
> * 명도가 낮을수록 검은색, 명도가 낮고 채도가 낮을수록 흰색

> * LAB
> * 사람 눈이 감지할 수 있는 색차와 색공간에서 수치로 표현한 색차를 거의 일치시킬 수 있는 색공간
> * L = 명도, A = Red + Green, B = Yellow + Blue
> * 노란색 차선을 인식할 때, B를 이용하면 좋은 성능을 내미

> * HLS
> * 색상 균형 HSV의 V(명도)를 L(밝기)로 바꾼 것.
> * H = 색조, L = 밝기, S = 채도
> * 밝기가 낮을수록 검은색, 높을수록 흰색
> * 흰색 차선을 인식 할 때, L을 사용하면 좋은 성능을 냄.

> * 차선 식별
> * 히스토그램 방법
> * 도로 이미지에 보정, 임계값 및 원근 변환을 적용하여 차선이 두드러지는 이진 이미지를 얻음.
> * 얻은 이진 이미지에서 어떤 픽셀이 라인의 일부이고, 이게 왼쪽라인인지, 오른쪽 라인인지 결정해야함 = 히스토그램 사용
> * 각 열에 따라 픽셀 개수를 더하면 히스토그램에서 가장 눈에 띄는 두 개의 peek가 나오고, 차선의 x위치를 파악가능함.

> * 슬라이딩 윈도우
> * 선 중심 주변에 배치된 슬라이딩 윈도우를 사용해서 프레임 상ㄹ단까지 선을 찾아 따라감.
> * 한 윈도우 안에서 감지되는 선의 중심을 기준으로 계속 윈도우가 쌓임.
> * 아래쪽 처음 블록은 앞선 히스토그램으로 정의되고, 이미지 아래쪽에서 위쪽으로 검색하면 올라감.
> * 슬라이딩 윈도우가 여러개 쌓이게 되면, 그 중심을 연결해서 선을 그림.
> * Polyfit을 사용해서 2차원으로 표현함. = ay^2+by+c=x
> * 2차식을 통해서 a, b, c 값을 구하게 됨.

> * 최종 변환 과정
> * 카메라 캘리브레이션 => Yellow, White 마스킹 => 버드 아이즈 뷰 및 이진화 => 히스토그램 및 슬라이딩 윈도우, Polyfit => 차선영역을 녹색으로 칠하기(Polygon)










