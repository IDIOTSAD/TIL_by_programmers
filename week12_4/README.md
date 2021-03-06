# 강의 요약

## 특징점 기술의 역사 톺아보기
### Pre-1980
* 1980년대에서는 깔끔한 이미지를 출력하기 어려움 - 초소형 센서 등이 미흡하였음.
* 2D -> 3D 세상을 이해한다는 목적이 지금과 비슷함.
* 이미지 속에서 어떤 정보를 추출해야 3D 세상을 이해할 수 있을까?
* 가장 활발한 연구는 라인 검출이었음.
* 노이즈를 찾기 위해서는 작은 객체의 검출보다, 이미지 전체의 패턴을 파악하는 방향으로 됨.
* 객체를 표현하는 경계, 라인을 추출하기 위해서 개발이 됨.
* 가장 유명한건 그래디언트 오퍼레이터
* 그래디언트 오퍼레이터 알고리즘을 기반으로 소벨 알고리즘이 만들어짐.
* 메모리 속에서 이어져있지 않은 이미지 속의 특색을 찾는 과정 (row, col 을 넘나드는 작업을 하기 어려웠음)
* 적당한 임계값을 넣어서 라인인지 아닌지에 대해서 진행하는데, 임계값을 찾기가 어려웠음.
* 컨벌루션을 이용해서 쉬운 임계값을 넣을 수 있는 소벨이 인기를 끌게 됨.
* 강한 라인을 찾기 위한 임계값 찾기는 여전히 어려웠음.
* 소벨 알고리즘에서 추가적인 방법을 이용한 허프 트랜스폼이 나옴.
* 소벨로 뽑아낸 엣지를 파라메터 스페이스에 표현함으로써 파라메터를 검출하는 방법
* 허프 트랜스폼을 기반으로 정확한 라인을 찾을 수 있게 되었고, 현재까지도 많이 쓰임
* 소벨 결과에서 엣지 다이렉트 정보와 히스토그램 정보를 통한 쎈 엣지를 찾는 기법인 캐니 엣지가 나옴. 
* 안정적인 강한 엣지를 찾을 수 있고, 알파값을 통해서 세기를 정할 수 있음. - 단, 느리다.
---
* 허프 + 캐니를 통해서 엣지 추출의 큰 획을 그을 수 있었다.
* 라인을 뽑음으로써 물체의 세멘틱을 추론할 수 있다는 프라이어가 많이 나옴.
* 프라이어를 이용해서 세그멘틱을 늘리는 연구가 발달됨.
* 멀리 찍은 객체를 같은 물체임을 인식 할 수 있을까?
* 라인을 추출해도, 라인과 연관성을 잇기가 어려웠음.
* 가까운 객체는 불변체 방향을 검사해서 구분 할 수 있지만, 비슷한 방향에서 바라보는 이미지에서는 토폴로지로 검출 가능
* 각도가 많이 틀어지거나 하면 연관성 찾기가 어려워짐.
* 라인이 아닌 다른 기하학 적인 방법을 찾음.
* 라인과 라인의 닥 프로덕트를 통한 교차점 (포인트)를 찾아서 피쳐를 찾는것.
* 라인과 라인의 크로스 프로덕트를 통해 찾는 방법

### Feature detector
* Point Feature - 키포인트와 디스크립터로 구성
* keypoint detector - 뽑은 포인트 피쳐의 픽셀을 의미함 (내가 뽑은 키포인트는 x = ~ , y = ~)
* descriptor extractor - 뽑은 포인트 피쳐의 특징 (특징 기술자, 키포인트 주변의 픽셀을 분석하여(패치를 땀) 디스크립터로 만듬 - 히스토그램으로 나타냈다)
* correspondence matcher - 2개의 포인트 피쳐가 같은 객체인지 결정하는 매칭 정보 (디스크립터 정보를 가져와서 2개의 포인트 피쳐 비교)
* local feature - 로컬 스케일로 이미지를 표현 할 수 있는 방법 - (포인터 피쳐도 있고, 라인 피쳐가 있을 수 있다.)
---
* Moravec - 포인트 피쳐의 조상격
* 한스 모라베 - 사람이 하기 쉬운 작업은 로봇이 하기 어렵고, 로봇이 하기 쉬운 작업은 사람이 하기 어렵다.
* Obstacle Avoidance and Navigation in the rael world by a seeing roboty rover 논문
* 이미지 속 코너를 찾아서 포인트 피쳐로 사용하는 내용이 나옴.
* 포인트 피쳐를 이용해서 연속된 이미지 사이에 로봇의 움직임을 추론하는 내용
* 이미지를 분석해서 코너를 찾는 가장 첫번째 논문.
* 픽셀의 기점으로 오른쪽, 오른쪽위, 위, 왼쪽위 그래디언트를 분석해서 코너인지 검사하는 것을 제안함.
---
* Harris corner

![image](https://user-images.githubusercontent.com/55529455/170863061-5cb7cb29-0638-48d1-9a99-c000ddb9e9df.png)
* x,y방향의 그레디언트만 하고, 이 정보를 이용해서 코너의 방향을 추측할 수 있는 매트릭스를 만듬.
* 이 후, 매트릭스 속에서 eigenvalue를 추출하고, 코너의 방향성으로 인지하여 코너를 좀 더 좋게 검출함.
* eigenvalue를 기반으로 스코어를 매겨 flat, edge, corner 검출을 제안했는데, corner 검출이 뛰어남.

---
* SIFT
* 딥러닝 방식 나오기 전 가장 정확했던 포인트 피쳐 기반 알고리즘
* 스케일링 인베일런스 (스케일 불변성) - 스케일이 변해도 잘 검출함 (scale -invariant)
* 로테이션 인베일런스 - 로테이션이 바껴도 잘 검출함.
* 이미지를 여러 스케일로 변환한 복사본을 가짐. - 이미지 피라미드
* 작은 스케일, 큰 스케일에서도 동일한 키 포인트가 추출되면 스케일 인베일런트 하다.
* 각각의 스케일마다 여러 가우시안 이미지를 만든다. (DOG)
* 스케일을 변화하는 시뮬레이션을 수행 - DOG를 분석하면 미세한 스케일 변화, 큰 스케일 변화에서도 스케일 인베일런트한 키포인트를 추출할 수 있다.
* 디스크립터도 제안함.
* 추출한 키포인트 주변 16x16픽셀만큼 패치를 만들어서 탐사함. - 그레디언트를 계산하고, 그레디언트에 대한 히스토그램 작성 후, 디스크립터를 만듬.
* 메모리, 많은 자원이 소요됨.
* 매칭이 매우 잘됨.
---
* FAST
* 빠르게 코너를 찾는 키포인트 디텍터.
* SIFT와 다르게 디스크립터는 없고, 해리스 코너처럼 코너만 찾을 수 있음.
* 엄청난 속도로 인해 많이 사용함.
* 해리스 17, SIFt의 42배의 속도.
* 2008년에는 머신러닝을 통해서 코너를 더 빠르게 검출하는것이 제안됨.
* 작동원리
* 찾으려는 픽셀을 중점으로 16개의 픽셀에 밝기값을 탐지함.
* 10개의 연속된 밝기가 6개의 밝기보다 더 밝으면 코너라고 인식
---
* BRIEF
* FAST와 잘 맞는 디스크립터
* SIFT처럼 float 방식이 아닌, 2진 값으로 표현하는 방식을 사용함.
* SIFT - 512 byte = 4096bit, BRIEF-256 = 256bit
---
* FLANN 라이브러리
* 2009년 발표, 수많은 디스크립터가 모여 있는 데이터에서 내가 방금 뽑은 디스크립터와 가장 비슷한 디스크립터가 있는지 매칭을 해주는 기능.
* 디스크립터 데이터가 고차원으로 되어있으므로 비슷한가 확인하는데에도 계산값이 많음. - 해시테이블을 사용할 수 없음.
* 트리 구조를 가지고 개발이 되었음.
* 비슷한 정도를 계산하는 eval과 더욱 가까운 디스크립터로 이동하는 기법이 필요하므로 문제가 되었음.
---
* ORB - 오알비, 오브
* SIFT의 정확도를 가지고, 실시간으로 작동하는 방식을 가짐.
* Oriented FAST + Rotated BRIEF
* FAST가 Scale invarience하지 않다는 점, BRIEF가 Rotation invariance 하지 않는다는 점을 개선하였음.
* SIFT 보다 몇십배 좋음.
* FAST 할 때, 이미지 피라미드를 추출하는 방식을 이용 - 추출할 때, 키포인트 주변 그레디언트를 이용하여 코너를 방향성을 찾고, 방향에 맞게 BRIEF를 줌.
* 어떤 방향에서 뽑던 코너의 방향에 맞는 BRIEF를 줌으로써 해결하였음.
* VSLAM 사용 시, ORB를 사용하게 된다면 매우 궁합이 잘 맞기 때문에, ORB가 VSLAM의 표본이 됨. 다른 모델쓸 때 ORB와 비교함.
---
* AKAZE
* 정확도와 성능을 비교 했을 때, ORB와 SIFT의 중간 정도
* 웬만하면 ORB를 사용하지만, 너무 빨리 계산되어 시간이 남는다면, AKAZE를 쓰는 경우도 있음.
---
* Local feature - SuperPoint, KeyyNet, HardNet
* 딥러닝 방식의 local feature
* 매칭을 극대화하는 loss function을 기반으로 수많은 데이터 셋에서 학습하는 방식
* 수준 높은 딥러닝 기반 - GT 데이터를 만들기가 매우 어려움.
* SIFT로 Annotation하면, SIFT보다 더 좋은 결과가 나올 수 없음.
* SuperPoint의 경우, OpenGL을 이용하여 인위적으로 렌더링한 정보에서 코너 정보를 Annotation으로 삼아서 기본적인 코너를 만듬.
* 이 후, 해당 그래픽에 호모그래피를 통해서 다양한 시점의 코너를 학습하기 위해 정보를 쌓음
* 실제 데이터에서 만듬으로써 self supervise deeplearning, domain transfer 방식이 한꺼번에 들어감.
* 키포인트 디텍터, 디스크립터 디텍터가 합쳐져 있음.

















