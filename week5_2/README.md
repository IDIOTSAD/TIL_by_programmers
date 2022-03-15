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

> * opencv API 도움말
> * http://docs.opencv.org/

# 2강 요약 (OpenCV 편하게 사용하기)
> * Image Watch = Mat 데이터를 이미지 형태로 보여주는 확장 프로그램.
> * 설치 방법 : Visual Studio 메뉴 - 확장 - 확장관리에서 Image Watch를 검색하여 설치 후, 재시작하면 설치됨.
> * 사용법 : 중단점(F9) 설정 후, 디버깅(F5) 시작. -> 보기-다른창-Image Watch 메뉴 선택 (확대 축소, 픽셀값 확인 가능)

> * 프로젝트 템플릿 = 프로젝트 속성, 기본 소스코드 등이 미리 설정된 프로젝트를 자동으로 생성하는 기능
> * Visual Studio의 템플릿 내보내기 마법사를 통해서 ZIP 파일로 패키징된 자신만의 템플릿을 만들 수 있음.
> * OpenCV 프로젝트 템플릿 = OpenCV개발을 위한 추가 포함 디렉터리, 추가 라이브러리 디렉터리, 추가 속성등을 미리 설정되어있는 콘솔 응용 프로그램 프로젝트 생성
> * OpenCV 기본 소스코드, 테스트 영상 파일도 함께 생성

> * OpenCV 프로젝트 만들기

![image](https://user-images.githubusercontent.com/55529455/158314692-a8a211d0-3ba9-4f4f-a79e-a52858c47ecd.png)

> * OpenCV 프로젝트 템플릿 사용
> * C:\user\(username)\문서\VisualStudioXXXX\Templates\ProjectTemplates에 생성된 프로젝트 템플릿을 넣는다.
> * 이후, 새 프로젝트에서 opencv 프로젝트 만들기가 생성 된 것을 알 수 있다.

# 3강 요약 (OpenCV 주요클래스 1)
> * Point 클래스
> * 2차원 점의 좌표 표현을 위한 템플릿 클래스
> * 멤버 변수 = x, y
> * 멤버 함수 = dot(), ddot(), cross(), inside() 등
> * 다양한 사칙 연산에 대한 연산자 오버로딩과 cout 출력을 위한 << 연산자 오버로딩을 지원
> * int, int64, float, double, point2i 등의 자료형을 지원
> * 사칙연산을 지원함.
> * norm 함수 = 좌표가 있을 때, 0 ~ 해당 좌표까지의 대각선의 길이를 구해주는 함수

> * Size 클래스
> * 영상 또는 사각형의 크기 표현을 위한 템플릿 클래스
> * 멤버 변수 = width, height
> * 멤버 함수 = area()
> * 다양한 사칙 연산에 대한 연산자 오버로딩과 cout 출력을 위한 << 연산자 오버로딩을 지원
> * int, int64, float, double 등의 자료형을 지원

> * Rect 클래스
> * 2차원 사각형 표현을 위한 템플릿 클래스
> * 멤버 변수 = x, y, width, height
> * 멤버 함수 = tl(), br(), size(), area(), contaions()
> * 다양한 사칙 연산에 대한 연산자 오버로딩과 cout 출력을 위한 << 연산자 오버로딩을 지원
> * int, float, double 등의 자료형을 지원
> * Size와 덧셈연산의 경우는 해당 좌표에서 크기가 늘어나고, point와의 덧셈연산은 좌표가 그만큼 shift를 하게 된다.
> * 비트 연산을 지원, &의 경우, 교집합을 의미하고, |의 경우는 합집합(두 네모를 합친 크기의 사각형) 을 의미한다.

> * Range 클래스
> * 정수 값의 범위를 나타내기 위한 클래스
> * 멤버 변수 = start, end
> * 멤버 함수 = size(), empty(), all()
> * start는 범위에 포함되고, end는 범위에 포함되지 않음. \[start, end)

> * String 클래스
> * 원래 OpenCV에서 자체적으로 정의하여 사용하던 문자열 클래스였으나, OpenCV 4.x버전부터 std::string으로 대체됨.
> * CV::format() 함수를 이용하여 형식 있는 문자열 생성 가능 -> C언어의 printf 함수와 인자 전달 방식이 유사

> * Vector 클래스
> * 벡터는 같은 자료형 원소 여러개로 구성된 데이터 형식 (열벡터)
> * Vec 클래스는 벡터를 표현하는 템플릿 클래스
> * cout 출력을 위한 << 연산자 오버로딩을 지원
> * 주로 16개 원소 이하를 갖는 열백터가 생성
> * Vec 클래스 이름은 재정의가 미리 되어있음.
> * Vec <num-of-data> {b|s|w|i|f|d}로 구성됨.
> * ex) Vec\<int, 2\> Vec2i
  
  
  
  
  
  
  
