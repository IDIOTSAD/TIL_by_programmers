# 강의 요약

> * 컴퓨터 비전
> * 컴퓨터를 이용하여 정지영상, 동영상으로부터 의미 있는 정보를 추출하는 방법을 연구하는 학문
> * 사과 사진을 보고, 둥글다와 빨간색이다, 사과꼭지가 있다라는 정보를 취득 할 수 있음. = 이를 통해 사과를 구분.

> * 컴퓨터 비전과 영상처리
> * 과거 = 영상처리는 영상을 다루는 모든 학문과 응용을 통틀어 지칭함. <=> 컴퓨터 비전은 영상인식과 같은 고수준의 영상 처리를 지칭
> * 현재 = 영상처리는 영상을 입력받아 화질을 개선하는 등의 처리를 하여 다시 영상을 출력을 내보내는 작업 <=> 영상처리는 컴퓨터 비전을 위한 전처리작업

![image](https://user-images.githubusercontent.com/55529455/160535911-6ff3d2ae-794d-40d7-8bdb-616706be28e2.png)
![image](https://user-images.githubusercontent.com/55529455/160535934-ac17e945-a2e4-494b-940f-629f2d48ba3d.png)

> * 카메라 & 컴퓨터가 영상을 인식하는 특성을 이해해야함 - 기울어진 글자, 격자 사각형 사이에 있는 점

> * 영상의 화질 개선
> * 카메라로 찍은 사진을 더욱 선명하게 만들거나, 색상을 원하는 형태로 변경하는 등의 작업
> * RAW 영상의 변환, 사진앱의 필터, 잡음제거, HDR, 초해상도 등

> * 내용 기반 영상 검색 (content-based image/video retrieval)
> * 영상에 존재하는 사람, 사물, 색상 정보 등을 인식하여 유사한 영상을 자동으로 찾아주는 시스템
> * 비쥬얼 검색

> * 얼굴 검출 및 인식
> * 얼굴 검출 : 영상에서 얼굴의 위치와 크기를 찾는 기법
> * 얼굴 인식 : 검출된 얼굴이 누구인지를 판단하는 기술 = 미세한 표정 변화, 조명 변화, 안경 착용, 헤어스타일 등
> * 의료 영상 처리 : X-ray 또는 CT 영상처리, 영상의 화질 개선, 영상의 자동 분석
> * 광학문자 인식 : 영상에 있는 OCR을 인식, 번역, 자동차 번호판 등 인식
> * 마커 인식 : 정해진 형태의 마커를 인식하여 숨겨진 정보를 추출, 2D 바코드, QR코드 등
> * 영상 기반 증강현실 : 카메라로 특정 사진을 가리키면 관련된 정보가 증강되어 나타나는 기술, 마커기반 & 비마커 기반

> * 머신 비전
> * 주로 산업계에서 제품의 위치 확인, 측정, 불량 검사 등을 위해 사용되는 영상 기반 기술. 공장 자동화
> * 빠른 처리 시간, 높은 정확도, 객관성
> * 카메라, 렌즈, 조명, 필터, 영상 보드, 영상 처리 소프트웨어 등으로 구성

> * 인공지능 서비스
> * 입력 영상을 객체와 배경으로 분할 - 객체와 배경 인식 - 상황 인식 - 로봇과 자동차의 행동지시
> * Computer Vision + Sensor Fusion + Deep Learning
> * 아마존 고, 구글, 테슬라 자율주행

> * 영상
> * 픽셀이 바둑판 모양의 격자에 나열 되어있는 형태
> * 픽셀 : 영상의 기본 단위, 화소 등
> * 그레이 스케일 : 흑백 사진처럼 색상 정보가 없이 오직 밝기 정보만으로 구성된 영상 (범위는 0 ~ 255)
> * 트루 컬러 : 컬러 사진처럼 다양한 색상을 표현 할 수 있는 영상 = Red, Green, Blue 색 성분을 각각 256개로 표현함. = 256^3

> * 그레이 스케일 영상의 픽셀 값 표현
> * 그레이 스케일 영상에서 하나의 픽셀은 0 ~ 255 사이의 정수값을 가짐 = 그레이 스케일 범위\[0, 255] 또는 \[0, 256}
> * C++ 에서는 Uchar로 표현함 (unsigned char)

> * 트루컬러 영상의 픽셀 값 표현
> * R, G, B 색 성분의 크기를 0 ~ 255 범위의 정수로 표현 0 = 검정, 255 = 흰색
> * Unsinged char 3개 자료형을 이용함.

![image](https://user-images.githubusercontent.com/55529455/160539031-dd0d75c1-e963-42f1-9c58-0adbecd15451.png)
![image](https://user-images.githubusercontent.com/55529455/160539054-c3f8ff77-544c-4edc-8ba1-fc30d9cdb463.png)
![image](https://user-images.githubusercontent.com/55529455/160539078-2e75f97f-c00f-47f9-9739-7fed0a8d3e8b.png)
![image](https://user-images.githubusercontent.com/55529455/160539104-b67fb5aa-7bb0-4ee1-bdc1-22f6b0d87955.png)
![image](https://user-images.githubusercontent.com/55529455/160539145-e080e76f-c48f-455c-b01b-c705d96d551c.png)
![image](https://user-images.githubusercontent.com/55529455/160539215-1896d8a9-c583-4b68-9099-93c0d2984327.png)

> * 비트맵
> * 비트들의 집합 = 픽셀의 집합
> * 영상 전체 크기에 해당하는 픽셀 정보를 그대로 저장함.
> * 장점 : 표현이 직관적이고 분석에 용이함.
> * 단점 : 메모리 용량이 많이 차지, 영상의 확대/축소 시 화질 손상이 심함
> * 사진, 포토샵

> * 비트맵의 종류
> * 장치 의존 비트맵 (DDB) : 출력 장치(화면, 프린터 등)의 설정에 따라 다르게 표현됨
> * 장치 독립 비트맵 (DIB) : 출력 장치가 달라지더라도 항상 동일하기 출력됨. BMP 파일은 Windows 환경에서 비트맵을 DIB 형태로 저장한 파일 포멧

![image](https://user-images.githubusercontent.com/55529455/160539486-ffcc4683-f771-499c-8da0-a7cc9caee5c3.png)
![image](https://user-images.githubusercontent.com/55529455/160539509-2902eff5-6cdd-4148-b6d2-f57cd9f0c0cc.png)
![image](https://user-images.githubusercontent.com/55529455/160539534-0eb10611-e072-426e-9799-8ec480f95cfe.png)
![image](https://user-images.githubusercontent.com/55529455/160539558-d95d4f33-5a10-49c9-9d39-b675ee50d71d.png)
![image](https://user-images.githubusercontent.com/55529455/160539630-b0635c1a-b988-497d-91c8-d07680758359.png)
![image](https://user-images.githubusercontent.com/55529455/160539659-f9a9e86c-08ae-4d1c-8d8b-03f52c6288b9.png)

> * BmpShow 프로그램
> * 마우스를 클릭하면, 해당 위치에 cat.bmp 파일에 들어 있는 비트맵을 출력하는 프로그램
> * windows 프로그램의 기본 동작 방식을 이해
> * bmp 파일을 디코딩하여 DIB를 출력함.

![image](https://user-images.githubusercontent.com/55529455/160539794-15c8c1ce-983f-49b9-8ac9-b8e9b66bd528.png)

> * 영상 데이터 크기 분석
> * 그레이 스케일 영상 크기 : 가로 x 세로
> * 트루 컬러 영상 크기 : 가로 x 세로 x 3






