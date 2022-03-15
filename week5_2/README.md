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
> * Vec \<num-of-data\> \{b|s|w|i|f|d\}로 구성됨.
> * ex) Vec\<int, 2\> Vec2i

> * Scalar 클래스
> * 크기가 4인 double 배열을 멤버변수로 가지고 있는 클래스
> * 4채널 이하의 영상에서 픽셀값을 표현하는 용도로 자주 사용
> * \[]연산자로 원소에 접근가능함.
> * gray, bgr, bgr alpha 표현 가능.

# 4강 요약 (OpenCV 주요 클래스 2)
> * 행렬 = 수나 기호, 수식 등을 네모꼴로 배열한 것, 괄호로 묶어서 표시

![image](https://user-images.githubusercontent.com/55529455/158322122-288526d5-b20c-405e-a9c3-2be5e321ede1.png)

> * 행렬의 기본연산

![image](https://user-images.githubusercontent.com/55529455/158322173-77f94c14-57f3-4b02-9996-d0cb7db212d6.png)
![image](https://user-images.githubusercontent.com/55529455/158322218-f46aafe9-48b8-4238-96e0-667334332abe.png)

> * Mat 클래스
> * N차원 1채널 또는 다채널 행렬 표현을 위한 클래스
> * 실수 혹은 복소수 행렬, 그레이스케일, 트루컬러 영상, 벡터필드, 히스토그램, 텐서 등을 표현
> * 다양한 형태의 행렬 생성, 복사, 행렬 연산 기능을 제공
> * 행렬의 생성시 행렬의 크기, 자료형과 채널수(타입), 초기값 등을 지정할 수 있음
> * 복사 생성자 & 연산자는 얕은 복사 수행(참조계수로 관리)
> * 깊은 복사는 copyTo, clone 함수 사용
> * 다양한 사칙 연산에 대한 연산자 오버로딩과 cout 출력을 위한 << 연산자 오버로딩을 지원
> * 2143번째 라인까지 되고, 이 위에 클래스 멤버변수가 정의되어있음. flag, dims, rows, cols, data등
> * dims = 행렬 차원, rows = 행, cols = 열, data = 데이터, size = 크기, step = 메모리공간의 가로크기

![image](https://user-images.githubusercontent.com/55529455/158324090-3a53a8cf-5d36-4fe9-bcf8-1a16ccb4f14c.png)

> * Mat 클래스의 깊이
> * 행렬 원소가 사용하는 자료형 정보를 가리키는 매크로 상소
> * depth() 함수를 이용하여 깊이 정보 받아오기 가능
> * CV_\<bit-depth>{U|S|F}

> * Mat 클래스의 채널
> * 원소 하나가 몇개의 값으로 구성되어 있는가?
> * channels() 함수를 이용하여 참조 - 그레이 스케일은 하나당 밝기 값 1개, 트루컬러는 3개

> * Mat 클래스의 타입
> * 행렬의 깊이와 채널 수를 한꺼번에 나타내는 매크로 상수
> * type() 함수로 참조
> * CV_(비트수)(정수형의 부호 S|U 또는 실수형 F)(채널 수)로 구성됨.

> * InputArray 클래스
> * 주로 Mat 클래스를 대체하는 프록세 클래스로 OpenCV 함수에서 입력 인자로 사용됨.
> * 사용자가 명시적으로 \_InputArray 클래스의 인스턴스 또는 변수를 생성하여 사용하는 것이 금지

![image](https://user-images.githubusercontent.com/55529455/158324899-98cae185-ce4b-4a67-a2a7-b46cb5c32522.png)

> * OutputArray 클래스
> * OpenCV 함수에서 출력 인자로 사용되는 프록시 클래스
> \_OutputArray 클래스는 \_InputArray 클래스를 상속받아 만들어져있고, create()함수가 정의됨.

# 5장 강의 (Mat 클래스 기초 사용법 1)
> * Mat 클래스 객체의 생성과 초기화 예제 코드

> * Mat 클래스 객체의 참조와 복사
> * Mat 객체에 대해 = 연산자는 참조(얕은복사)를 수행함.
> * Mat clone, copyTo 함수를 이용하여 깊은복사 수행해야함.

> * Mat 객체에 대해 () 연산자를 이용하여 부분 영상 추출 가능
> * () 연산자 안에 Rect 객체를 지정하여 부분 영상의 위치와 크기를 지정
> * 참조를 활용하여 ROI(Region of Interest) 연산 수행 가능.

# 6장 강의 (Mat 클래스 기초 사용법 2)
> * Mat 영상 픽셀 값 접근
> * 기본적으로 data 멤버 변수가 픽셀 데이터 메모리 공간을 가리키지만, Mat 클래스 멤버변수 이용을 권장

![image](https://user-images.githubusercontent.com/55529455/158326671-f6548b7a-d8a9-4932-b4f2-d915226bf0dc.png)
![image](https://user-images.githubusercontent.com/55529455/158326760-5cff63c6-ecef-4429-9807-7f6c7919f71a.png)
![image](https://user-images.githubusercontent.com/55529455/158326814-33638874-dcc8-4dd4-98c1-f1a27294e865.png)
![image](https://user-images.githubusercontent.com/55529455/158326894-bf57c778-219d-416c-9769-c87ed8ca2271.png)






