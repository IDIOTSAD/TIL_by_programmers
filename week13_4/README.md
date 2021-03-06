# 강의 요약
## mono SLAM (2003)
* 2003 년에 가장 초창기 SLAM (Davison)
* V-SLAM이 가능하다고 제안이 되었던 논문
* V-SLAM 파이프라인, 영상처리 테크닉이랑 다른 결을 타고 있는 알고리즘
* 그러다보니 세세한 기술은 파고 들어가진 않음.
* Incremental SLAM을 사용함. (요즘은 batch), EKF 필터를 사용함.
* 그 당시에 있었던 SLAM - 2D 라이다를 기본으로 하는 경우가 많았음. 파티클필터나, EKF를 많이 사용함.
* SLAM은 위치추정에 굉장히 정확하게 부합하는 문제임. - 위치추정을 위한 엔진으로 필터를 사용.
* EKF 엔진을 사용해서 3D 랜드마크와 카메라 pose를 트래킹함. - batch SLAM에서는 트래킹하는게 아니라 한꺼번에 계산한다.
* 3D 랜드마크는 한 시점에 보이는 2D 키포인트들을 옵티컬 센서를 기준으로 ray를 생성.
* ray를 생성하면, 어딘가에 keypoint가 있을텐데, 이를 EKF 필터를 통해서 가우시안 분포로 나타냄.
* 분포를 이용하여 Z 길이를 추정함. - 2D 키포인트를 가지는게 아닌, 3D 랜드마크 자체가 피쳐가 되는 것.
* 처음 시작 할 때는 알아 낼 수 있는 방법이 없다 - 기준점이 되는 랜드마크가 없음.
* 따라서 전제조건으로, 처음 생기는 맵은 depth를 알고 있어야하는 점이 있다. - 몇개의 객체에 대해서 알고 있어야 함.

## PTAM (2007)
* 2007년에 제안된 SLAM (Klein, Murray)
* mono SLAM이 2007년에 공유가 됨. + PTAM의 논문과 코드가 공유됨. - 굉장히 큰 히트! 실시간 사용가능
* PTAM은 Batch SLAM을 사용하였음. bundle adjustment 을 사용하여 최적화되어있음.
* Incremental SLAM, Batch SLAM을 비교할 수 있게 되어 비교 하게 됨. - PTAM 우승!
* CPU의 듀얼코어의 등장으로 인해, 멀티태스킹을 할 수 있게 됨. - PTAM은 이를 적용함. (Tracking, Mapping)
* Tracking을 빨리 빨리 돌아야함. Mapping은 Tracking보다 훨신 오래 걸린다. - 이를 해결하려고 했지만, mapping을 줄이면 정확도가 떨어지고..
* 이로 인해서 방 안에서만 SLAM이 가능했었다.
* PTAM에서는 이 둘을 분리하여 스레드를 할당시켜 동시적으로 작업되도록 하였음. - Mapping은 Realtime으로 안돌아도 되므로 느리지만 정확성을 높이게 하였음. (끊기진 않게)
* monoSLAM은 몇개 포인트를 메뉴얼하게 뽑아줬어야 함. (사전 정보 필요)
* PTAM은 모르는 정보로 시작 가능함. 하지만, manual init로 인해 epipolar geometry를 만들 때, 두개의 이미지를 사용자가 골라줘야했음.
* 5-point 알고리즘 써서 F-matrix를 구해서 R,T를 구하고 이를 기반으로 맵을 만듬.
* FAST Corner 검출 알고리즘을 사용하였음. (2006) - 이 때 당시에는 깜놀. SIFT보다 빠르다..
* 맵을 최적화 하는데 키프레임이라 하는 프레임을 가지고 번들 애드저스트멘트를 사용
---
* PTAM의 파이프라인
* key-frame - 이미지들이 빨리 들어오는데, 모든 이미지를 bundle adjustment 하면 계산량이 너무 많음. 맵을 추론하기 좋은 프레임만 가지고 하는 것.
* 띄엄띄엄 떨어진 프레임만으로 해도 되는데, 내부에서 휴리스틱을 이용하여 정의함. - 일정량의 새로운 피쳐가 갱신될때마다 키프레임으로 지정.
* 70% 정도가 이전 피쳐고, 30%는 새로운 피쳐다
* 새로운 키프레임이 아니면 맵을 그리고, 새로운 키프레임이면 새로운 점에 대해서 새로운 랜드마크를 추가 해줌.
* 에러를 계산해줌. 

![image](https://user-images.githubusercontent.com/55529455/171568389-acbb3bd4-7203-422f-aaf4-bfe1dad9977d.png)

---

## Visual-SLAM, why filter? (2012) (Strasdat)
* 왜 필터를 쓰냐? 구린데.. 이런 의미를 담은 논문
* 그래프 기반 최적화를 하는 방식이 왜 필터링 방법보다 더 효율적일 수 밖에 없는가?
* V-SLAM은 EKF, PF 쓰기전에 BA를 써라. - 동일한 정확도를 얻기 위해서 필터링은 많이 돌려야하고, BA는 한번에 batch하여 계산함.
* 의외로 BA가 계산량이 적음. - 이 논문 후로는 BA를 사용함.

## ORB-SLAM (2015)
* 2015년 Mur-Artal이 제작함.
* 딥러닝에 YOLO가 있다면, SLAM에서는 ORB-SLAM이 있다.
* 개인적으로는 ORB-SLAM으로 하기에는 너무 어려움. - 기반 지식이없으면 어렵다.
* 가장 유명한 이유는 VSLAM pipeline을 완벽하게 시스템을 구현함. - 모든 기능을 다 갖춤.
* 성능이 좋은가? - 그건 모르겠음. 실시간에서 돌아갈 수 있는 정도로 맞춰짐.
* 웬만한 use-case를 통과 할 수 있을 정도로 완성되어있음.
* PTAM에서는 2개의 코어 멀티프로그래밍을 했다면, ORB 때는 4~6개 코어 스레드를 이용 할 수 있게 됨.
* 트래킹(매 프레임), 로컬 매핑(100~200ms), 루프 클로저(루프를 돈다면.. 몇초) 3개의 스레드로 구성
* user input이 절대 필요하지 않음. - PTAM은 1개의 epipolar geometry를 만들어지기 위한 view를 제공했어야 했음. (어떤 프레임을 잡아야 init map이 좋게 나오는지 풀지 못해서)
* 어떤 풀이로 좋은 프레임을 풀어서 좋은 맵을 만들 수 있는지 스스로 평가 - 좋은 맵이 안생기면 SLAM을 재시작하는 Automatic map initialization
* PTAM에서는 눈을 가렸다가 다시 돌아와도 매칭이 된다. - PTAM의 한계는 잃어버렸던 위치로 다시 돌아와야함. (마지막으로 잃기 전 데이터)
* ORB-SLAM은 다른 위치에서도 트래킹이 됨. 한 번 스캔이 됐다는 전제가 있으면 됨. - Relocalization + global optimazation (loop closer)
* ORB-feature를 사용함.
* 2가지의 그래프를 가짐.
* 1. Co-visibility graph
* 2. Essential graph
* 왜 다른 형태를 가지나? - 계산 효율성을 위해서 (많은 데이터를 가지는게 정확한 정보를 추출 할 수 있고, 속도때문에 중요한 데이터만 이용하는지)
* Relocalization할 때, Bag-of-visual-words를 사용함.
---
* ORB-SLAM pipeline
* 프레임에서 ORB 뽑고, 처음 map을 만듬.
* 다시 프레임으로 돌아와서 프레임에서 ORB 뽑고, 최근 키 프레임가지고 초기 위치 추정. EPMP를 써서 맵을 기반으로 위치를 트래킹함.
* 로컬 맵 트래킹 수행하고, 새로운 키 프레임이 나오면, 키프레임에 넣고, 컬링하고, 새로운 맵포인트를 만들고, local BA를 함.
* local BA - 1000개 프레임으로 BA하면 데이터가 엄청 많아질 것이다. 실시간에 불가능함. 가장 최근에 n개의 키 프레임만 가지고 BA 하여 업데이트 한다는 것.
* 그 이전의 것은? 그대로 나눈다. 이미 좋은 데이터라고 판단하는 것. 최근의 것은 Need Optimization.
* loop 인지 아닌지 구분 하고, 루프라면, 최적화를 해줘버림. 랜드마크 업데이트는 안하는듯.

![image](https://user-images.githubusercontent.com/55529455/171588893-23e741f2-6df5-4d4d-b2be-e9c7e10cf818.png)

---
* ORB features를 써서 FAST를 쓰고, BRIEF를 써서 (located BRIEF) 만듬.
* Automatic initialization
* Homography solver - Panar scene - 평면의 씬에 대해서 맵을 만들때 좋음.
* Fundamental matrix solver - Complex scene - 울퉁불퉁한 씬에 대해서 맵을 만들때 좋음.
* 카메라에서는 울퉁불퉁한지, 평면인지 알 수가 없음. 따라서 2개를 써서 임계값을 줘서 결정함.
* epipolar geometry를 만들때 상하 베이스로 있어야하는데, 앞뒤 베이스는 생기지 않음.
* 이는, init map을 만들때는 잘못만들어지면 프로그램을 껏다 켜야하는데, 이를 판단하는 기능이 생겼다 볼 수 있음.
---
* Co-visibility graph (co-같이, visibility-가시성) - 사진 b
* 서로 바라보는 랜드마크가 분명히 있는데, 동일한 객체를 바라보는 키프레임끼리는 연관된 데이터 셋이 있을테니 표시를 해주는 것.
* 동시에 같이 바라보고 있는 것에 대한 그래프
* Essential graph - 사진 c
* 정말 중요한 데이터 셋만 남겨놓는 것. 

![image](https://user-images.githubusercontent.com/55529455/171590902-9ac17da5-6e01-44f2-8c5d-bd18336066c6.png)

---
* Relocalization
* Bag-of-visual-words - ORB feature를 이미지에서 뽑아서 클러스터링 해서 비슷한 이미지끼리 학습 시켜놓음. 
* 새로운 이미지가 있을 때, feature를 뽑고, bag-of-visual-words로 바꿔서 매칭하면 빠르게 구할 수 있다.
* vocabulary로 만들어서 트리 구조로 만듦. 실제 데이터가 들어왔을 때, 트리 searching 해서 어떤 비쥬얼 워드인지 확인함.

![image](https://user-images.githubusercontent.com/55529455/171591749-56043168-4e38-430b-bcc4-50b27f63d77e.png)

## ORB-SLAM2 (2017)
* 1에서는 좋은 설명 비디오가 없음.
* 1에서는 monocular 카메라를 썼다면, 2부터는 stereo, RGB-D 카메라 사용함. 조금 더 안정적인 알고리즘을 넣음.
* stereo는 처음부터 depth를 알기 때문에 조금 더 정확하게 SLAM을 할 수 있게 됨.
* RGB-D는 조금 다름. dense하게 뽑아내는게 있는데, ORB-SLAM은 단순히 RGB이미지에서 피쳐를 뽑은거에서 depth를 초기화 해주는 정도만 씀.

## ProSLAM (2018) (Schlegel)
* 성능이나 새로운 방법론 보다는, SLAM 엔지니어로써 시스템을 만들어야하는데, 시스템 아키텍쳐가 굉장히 좋음.
* 처음 공부할 때 이걸로 하면 좋다!

![image](https://user-images.githubusercontent.com/55529455/171593628-80540f96-6e6b-42f5-a2f6-49c2c73327aa.png)









