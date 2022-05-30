# 강의 요약
## 왜 2d geometry가 필요한가?
* 3D 월드 좌표를 카메라 프레임으로 옮기고, 2D 좌표로 매핑하는 과정을 알아봄. (3D -> 2D mapping)
* 반대의 경우는? intrinsic와 extrinsic의 Inverse를 통해서 구할 수 있을 것이다.
* 하지만, 실제 세상에서 extrinsic를 아는 경우가 없음. extrinsic을 아는 경우는 3D 포인트 x의 위치를 알고 있다는 것이다.
* intrinsic를 알아도, extrinsic를 알지 못하니 depth를 살리지 못함.
* RGB-D 카메라의 경우는 depth가 주어짐. - 이경우는 3D 포인트 위치를 이미지 하나로도 바로 알 수 있음 - SLAM을 안해도 되는거 아닌가?
* 실제 depth의 값이 요동치는 경우가 많음. - 보정하기 위해서 여러장의 이미지를 통한 V-SLAM을 이용함.
* depth가 있다면 2D -> 3D 공간으로 매핑이 가능함. 
* 2D -> 3D는 1장이 필요하지만, 3D -> 2D는 2장의 사진이 필요함
* 카메라를 이용해서 어느정도 이동했는지를 알아야함. - 이미지 간, 프레임마다 Pose 이동 데이터를 구하는 것
* 모션센서를 통해서 바로 알 수 있지만, VSLAM에서는 Visual 정보만으로 (영상) 추론 할 수 있어야함.
* 2개의 이미지를 기반으로 기하학적 상관관계가 어떻게 되는지 아는게 필요함.

## Epipolar geometry
* 우선, 2-view geometry를 알아보자. (2개의 이미지가 있는 경우)
* monocular는 한쪽은 과거, 한쪽은 현재로 받아서 하는 경우도 있음.
* monocular, stereo에서도 사용 할 수 있음.
* Epipolar line - 중요한 개념.
* 3D 이미지를 2D 이미지로 투영하는 과정에서 optical center에서 직선을 그리게 된다면, image plane에 x 상이 맺힘.
* 앞으로의 이 직선은 ray라고 함. (그래픽 계열에서 레이트레이싱) VSLAM에서는 3D point가 2D projection 될때 직선을 의미
* 이 ray를 오른쪽 카메라에서 보게 된다면, 투영이 될 것이다. - 재투영이라고 함. (re-projection), 2D 이미지 점을 3D 형태로 바꾼 후, 다시 다른 시점으로 2D로 투영했기 때문.
* ray가 재투영 된 직선을 Epipolar line라고 함.
* 왼쪽 카메라, 오른쪽 카메라가 동시에 바라보는 3D 좌표가 있다면, 무조건 Epipolar line가 있기 때문에 중요함.
* 어느 한 포인트를 보고 한 카메라에 투영이 되었다면, 다른 카메라에서 그 3D 포인트는 어떤 픽셀에 나오게 될 것이고, 무조건 Epipolar line 안에 있을 것.
* 카메라의 Rigid by motion을 찾기 위해 (각각의 optical center의 rotation, translation 차이를 알기 위해서) 각각 x를 보게 된다면, 무조건 Epipolar line 안에 있다.

![image](https://user-images.githubusercontent.com/55529455/170917851-c4bca372-6320-4743-94ca-201a8d07565c.png)
* Epipole
* 각각의 상에 맺힌 점 x에 대해서 ray를 그리게 되고, 다른 카메라에서 재투영을 해보자.
* 이 때, 각각의 ray가 다른 카메라에서 Epipolar line이 서로 intersection 하게 되는데, 이 점을 epipole이라고 한다.
* 이 epipole은 반대편 optical center와 같은 점이 되게 된다. - 반대편 optical center의 투영

![image](https://user-images.githubusercontent.com/55529455/170920617-db371609-6fdc-4a57-b321-ce1ea89489c6.png)

---
* 특수한 경우
* 전방 스테레오 카메라 - 두 카메라가 같은 방향을 바라보게 될 때
* 오른쪽과 왼쪽 서로 카메라를 바라볼 수 없기 때문. Epipolar line이 평행하게 나타나게 됨.
* intersection 하지 않기 때문에, 무한의 거리를 보게 되기 때문에, epipole이 생성되지 않는다.
* 카메라 위치를 조금씩 warp 해주면서 이 상황을 일부러 만들게 됨.
* epipole line이 가로로 나타나게 됨 - x1, x2, x3를 찾기 위해서는 다른 카메라에서 일부 row 안에서 찾을 수 있다.
* 굉장히 빠르게 데이터를 찾을 수 있는 장점이 있다. - 스테레오 매칭도 쉽게 할 수 있음.

![image](https://user-images.githubusercontent.com/55529455/170934721-d36552a7-e1c8-4cf0-8ad2-15610465714a.png)

---
* 특수한 경우 2
* 하나의 이미지가 회전 없이 직진만 한 경우
* monocular, 자동차에서 보이는 현상
* 두 epipole은 보이지 않지만, epipole line들은 방사형태로 보이게 됨.
* 원래라면 방향에 맞게 만들어지기 때문에, 반대 방향에는 안생겨야하는 게 아닌가? - ray는 방향성을 가지기때문에 (위치를 특정할 수 없음)
* 투영되는 시점으로 본다면 앞에 있다 뒤에 있다의 판단은 3D의 정보이기 때문에 앞에 있을지 뒤에 있을지 확정 지을 수 없음.
* 빠르게 데이터를 찾을 수 있게 해줄 순 없다 - 반대 방향이 없으면 더 빨리 인덱싱이 되는데, 그럴 수 없기 때문에.
* 하지만, epipole의 시점으로 본다면, e1, e2가 같기 때문에 어렵게 따로 구하지 않아도 된다. (0, 0, 0)
* 센서에서 나온 translation 값을 그대로 써도 된다는 장점이 있다. (따로 기하학적인 해석이 없어도 됨.)

![image](https://user-images.githubusercontent.com/55529455/170936437-0cd75bf5-44a3-49c1-811f-bb7e6d43bcac.png)

---
* 다시 원래대로 돌아와서 본다면,
* 아래 사진은 x를 기준으로 각각 투영된 값에, optical center를 연결한 것.
* epipolar plane은 epipolar line, epipole이 모두 포함.
* baseline - 각 카메라의 optical center를 연결했을때 생기는 직선 (두 카메라간의 거리 개념)
* baseline이 크면 클 수록 삼각측량이 정확해진다.
* baseline이 epipolar plane과 카메라 image plane과 겹치는 부분이 있다 - epipole
* epipole은 baseline 위에 있다는 것을 의미함.
* 하나의 이미지에서 여러개의 3D pointer를 인식 할 수 있다.
* x의 위치를 조금씩 위치를 바꾸면? - 각각의 epipolar plane이 생기는데, 이 때 baseline을 중심으로 회전하게 된다.
* 존재 할 수 있는 epipolar plane의 가능성이 많아지는데, 모든 가능성들을 epipolar pencil이라고 함.
* 1. 3d plane x는 epipolar plane 안에 있어야함.
* 2. epipolar plane은 epipole과 교차해야함.
* 3. 모든 baseline은 epipole과 교차해야하며, epipolar plane은 baseline을 포함하고 있어야함.
* 이러한 조건을 지오메트리 컨스트레이트이라고 함. (에피폴라 컨스트레이트)

![image](https://user-images.githubusercontent.com/55529455/170939436-5b94efaa-0b38-491f-bb01-29d0c5428c88.png)
![image](https://user-images.githubusercontent.com/55529455/170941094-32e2a7ff-27d4-494a-88d1-39b9da950617.png)

## Essential / Fundamental matrix
* E-matrix (Essential)은 epipolar constraint에 대한 정보를 담고 있는 매트릭스. 3x3
* 카메라 모션을 정확히 추론하는 것이 중요하기 때문에, E-matrix를 얻어내는 것이 중요함.
* 해당 식을 사용할 때, x의 값을 모르기때문에 계산 할 수 없다.
* E-matrix를 표현할때는, normalize image plane으로 표현함.
* 실제 이미지를 다룰 때는 픽셀로 표현함. - normalize image plane에서 pixel image plane으로 변환 해야함.
* 하나의 카메라로 모션을 추정할때, 좌우 모두 동일한 k-matrix를 가지지만, 스테레오는 서로 다른 k 매트릭스를 사용함.
* 각각의 다른 카메라에 맞는 k-matrix를 써야함.
* 왼쪽 오른쪽에 k-matrix의 역행렬을 넣는데, 이렇게 만들 경우, Fundamental matrix라고 부르게 된다. (E-matrix에서)
---
* Epipolar line과 point가 intersection이 된다면, 이 두 값의 dot product는 0이다.
* 이를 이용하여 T, R을 빠르게 찾을 수 있음.
* x와 Fundamental matrix의 dot한 값에, x'를 곱했을때, 0이되는 값을 찾으면 됨.

![image](https://user-images.githubusercontent.com/55529455/170943640-4f5d0ff2-552d-43d1-a965-da2c2f1d5bf2.png)
![image](https://user-images.githubusercontent.com/55529455/170945395-8c324554-e49d-4767-9896-25f74466a206.png)
![image](https://user-images.githubusercontent.com/55529455/170945694-483f82b4-cb75-4b6d-8835-c24ffb74c868.png)

---
* 8-point algorithm - 최소 8개의 Corresponding Points 가 있을 때, F-matrix
* 5-point algorithm - 최소 5개의 Corresponding Points 가 있을 때, E-matrix
* F-matrix는 7개의 자유도를 가진다. (tx, ty, tz, rx, ry, rz, focal length, Corresponding Points) 8개가 있다고 볼 수 있지만, scale을 구할 수 없음. 따라서 8-1
* E-matrix는 5개의 자유도를 가짐. (tx, ty, tz, rx, ry, rz) 6개 사용. 이 역시 scale을 구할 수 없기 때문에 6-1 = 5개
* minimal solver - 추론하기 위해서 필요한 데이터 수가 필요하기 되는데, 최소한의 데이터로 문제를 해결하는 것.
* 5-point 5개의 데이터를 추론하기 위해 5개의 데이터를 사용하기 때문에 minimal.
* 8-point 7개의 데이터를 추론하기 위해서 8개의 데이터를 사용하기 때문에 non-minimal
* 7개의 데이터를 사용하기 위한 방법은 있지만, 작동하지 않는 조건도 있기 때문에, 8개로 사용함.

![image](https://user-images.githubusercontent.com/55529455/170948130-b0a78cf5-c89c-48ba-a3c2-83b0cb39a73b.png)
* 해당 사진에서는 x'와 x''를 알게 된다면 이를 행렬을 만들 수 있다. 큰 A 매트릭스. (각 쌍에대한 데이터가 들어감)
* 데이터가 노이즈 껴져 있다면, 0이 아니라 ax+b가 나오고, 이 식에서 최소가 되는 값을 구하면 됨.
* F, E 둘다 해당 방법을 따라가지만, 중간 매트릭스 랭크나 컨스트레이트를 넣어주는 부분때문에 5, 8로 나뉘게 됨.
* 5, 8 모두 opencv에서 제공함.
* findFundamentalMat() - F-matrix
* recorverPose() - E-matrix
* Correspondence 여태까지 얘기했던 거는 무엇일까? - 지난 시간에 배웠던 피쳐 디스크립터의 매칭정보임.
* 피쳐마다 ID가 있고, 디스크립터와 매칭한 정보를 담음.
* 매칭을 한 후, 이 함수에 넣으면 사용 가능함.

![image](https://user-images.githubusercontent.com/55529455/170949146-1e91fed4-e640-42f8-adee-cd4503279754.png)

## Outlier removal
### Outlier rejection
* SLAM 의 데이터는 2가지로 나뉨.
* Inlier data - 좋은 데이터 : 관측 시 예상했던 데이터 분포수를 잘 들어 맞는 데이터
* Outlier data - 나쁜 데이터 : 데이터의 분포에서 현저하게 벗어나있는 관측 데이터
* 보통 데이터 분포 모델에서 부터 얼마나 에러값을 가지는지 판단. - 모든 데이터는 노이즈를 가짐.
* 단순히 에러값으로만 판단 할 수 없음. - 올바른 이미지임에도 높은 노이즈로 인해 에러를 가진다면?
* 검출된 픽셀에 F-matrix 곱하면 오른쪽의 Correspondence 위치가 나옴.
* 디스크립터 결과가 나왔다 해도, F-matrix 했을 때, 오류가 나옴을 확인할 수 있음.
* F-matrix의 검증을 통해 Inlier, Outlier 결과가 나옴.
* Outlier 가 나오는 전제조건 - 급격한 조명, 회전, 가림, 모션블러와 같이 깔끔한 데이터 못얻거나, 기하학 조건이 깨질때
---
* 컴퓨터 비전에서의 2가지 종류의 알고리즘
* Closed-form algorithm - 수많은 미니멀 알고리즘, 정확한 기하학적 조건을 가지고 있을 때 작동되도록 설계됨. (8-point)
* Iterative optimization - 많은 데이터 가지고 있을 수 있지만, 모든 데이터가 1개의 결과가 나올때까지 반복함. 패턴을 찾는 것이 목적. 분포를 따르지 않는 결과가 있다면 잘못될수도.
* 오염된 raw data에서 outline을 제거하여 깔끔한 inline 데이터만으로 계산할 수있도록 만드는 것이 중요.
---
* ex) line fiiting (linear regression)
* linear regression - 2d plot에서 여러개 데이터 있을때, 가장 정확한 직선을 가로지르는 것을 찾는 것.
* 어떤 직선이 더 정확하게 가로지르는가? 척도가 필요함.
* SSE - Sum of squared error = 거리의 제곱근
* SAE - Sum of absolute error = 거리의 절대값
* 이 데이터 셋에 outlier가 있다고 하자.
* 그래프를 봤을 때, M1이 더 정확한 데이터 일 것이다. - 4개가 사람이 봤을 때, 통계적으로 더 높기 때문에.
* 알고리즘 입장에서는 뭐가 이상한지 모름 - 4개 점이나 1개 점 모두 같은 데이터.
* 4개의 점의 오차보다 1개의 점 오차가 크기 때문에 M2가 에러치가 더 낮음.

![image](https://user-images.githubusercontent.com/55529455/170965665-fc0d219d-2150-41f9-b5d7-f12e82557b8a.png)

* 데이터 사이에 outlier가 있으면 오류 수정이 어려움.
* 단 하나의 outlier 때문에 잘못된 추론이 나올 수 있다.
* 이전엔 20% outlier지만, 실제로 80% outline의 경우에도 추론이 가능해야함.

## RANSAC
* Fischler & bolles가 개발한 알고리즘
* Random Sample Consensus
* Random - 무작위하게
* Sample - 데이터 샘플을 뽑아 모델을 만들고
* Consensus - 모델에 대한 데이터의 합의도를 알아봄
* 모델은 무엇이지? - RANSAC은 템플릿 알고리즘이기 때문에, 프레임워크 뿐이고, 실제로 안에서 돌아가는 알고리즘은 따로 있다.
* ex) homography, essenital matrix, fundamental matrix
* 정확하게 추론하고 싶어하는 결과를 뜻하는 것.
* fundamental matrix로 예시를 들면, input 데이터에 outlier 데이터가 껴있으면 8-point가 잘 동작하지 않음.
* 따라서, input 데이터를 랜덤하게 뽑아서 fundamental matrix를 구하고, 다른 데이터도 구해서 정확하게 뽑았는지 평가를 수행함. - 이러한 과정을 모델 추론이라고 함.
---
* RANSAC 작동방식
* 랜덤하게 minimal set of data(모델 실행을 위한 최소한의 데이터 수)를 뽑음 - ex) 8-point는 8개 데이터를 뽑음.
* 뽑은 데이터를 기반으로 모델을 추론함.
* 모델 스코어를 측정함. (알고리즘마다 다름, Current score > so-fat-best-score 이면, update score)
* 계속 반복한다.
---
* Homography RANSAC 작동방식
* 4개의 피쳐 데이터를 뽑음. - 4쌍의 피쳐 매칭이 필요하기 때문에
* 뽑은 데이터를 기반으로 호모그래피 매트릭스를 추론함. - 왼쪽 이미지의 픽셀값에 호모그래피 매트릭스를 곱해봄.
* 오른쪽 이미지 feature consensus 위치에 픽셀이 올라오는데, 데이터에 노이즈가 있으면 정확하게 안되어 있을 것임.
* 해당 픽셀의 거리 차이만큼의 에러만큼 모두 더하면 reprojection error 라고 함.
* 특정 거리 값에 대한 임계값을 지정해서 (2픽셀 이상 떨어진것을 에러라고 한다던가..)
* Current score > so-fat-best-score 이면, update score
* 계속 반복한다.
---
* 언제까지 돌려야하는가?
* T는 우리가 돌려야 할 최적의 루프 횟수
* P는 우리가 뽑은 모델이 모두 inlier으로 이뤄줘야할 확률
* E는 전체 데이터 수의 inlier, outlier의 수
* S는 매 루프마다 샘플링 해야 할 수

![image](https://user-images.githubusercontent.com/55529455/170981415-7ab8e98c-3a78-4474-9385-b7d19acf86f6.png)

* RANSAC 장점
* 성공 하면, inlier 만으로 로 모델을 추론하고, 데이터셋에서 outlier을 제거 할 수 있음.
* 전체 프로세스 시간을 예측할 수 있다.
* 언제 끝날 지 알 수 있다. - 성공과 실패를 구분 하는 좋은 지표
* 이해하기 쉽다.

* RANSAC 단점
* 랜덤성 알고리즘으로 결과값이 다르게 나옴 - 동일한 데이터 셋으로도 성공 실패가 갈림.
* 전체 데이터셋의 inlier 보다 outlier가 많으면 실행시간이 엄청 늘어남.
* 실패하게 되면, 모든 가능성을 고려하게 되는 방향으로 수렴하게 됨.
* 하나의 데이터 셋에서 여러 데이터 모델을 추출 할 수 없음.


## Modern RANSACs
* 기존 RANSAC의 한계로 인해서 해결할 수 없는 점들이 있음.
* 기존 RANSAC이 단순하기 때문에 조금 수정하면 모델 추론이 더 빨라지고 안정적으로 됨.
* 데이터셋의 분포 알고있어도, 모델 추론의 prior 정보가 있어도 활용할 수 없었음.
* 샘플링된 데이터에 노이즈가 있어도 노이즈가 없는 것처럼 다뤄지는 경우도 있었음.
* 요즘 컴퓨터 비전 튜토리얼에서 RANSAC은 구리다라고 할 정도로 바뀜.
* 개량 RANSAC에 대한 정보를 알아보자.
---
* 개량 RANSAC에 대한 배경상황
* 대부분 모른다!
* OpenCV에서 사용하는 RANSAC은 스탠다드임.
* OpenCV 4.5 버전에 RANSAC 개량 버전이 들어왔음.
* 개량 RANSAC은 종류가 많다. 다양한 것들을 공부해보고, 적합한 것이 무엇인지 결정해야함.
* 여러 방법론의 장점을 따와서 커스터마이징 가능함.
* PROSAC, Lo-RANSAC을 조합해서 하는 방법이 강사님의 추천
---
* Early-stop method - 운좋게 RANSAC을 바로 찾았을 때, RANSAC을 끝내는 것. (자원을 아낄 수 있다.)
* 3가지 변수를 미리 정해놔야함.
* minimum iteration - 최소한 돌아야 하는 반복 횟수
* maximum iteration - 최대한 반복 횟수 - 일정 횟수 이상이면 실패했다고 하는 것.
* success score - 성공 지표 - 이 지표를 넘어서면 성공이라 판단, 탐색 종료
---
* PROSAC
* 매칭에 특화된 RANSAC, data prior를 잘 이용한 예시
* 전제 조건 : 디스크립터 매칭측정 a2_norm, hamilton_distance을 측정하는데, 피쳐 디스크립터간 디스턴스가 적은 매칭일수록 모델 추론때 더 정확히 추론될 가능성(inlier 가능성)을 봄.
* Random Sampling 과정을 좀 더 낮은 디스턴스를 가지는 디스턴스 매칭 샘플링으로 바꿈.
* 점점 더 높은 distance를 가진 디스크립터 매칭 샘플링 기법을 사용.
* 프로그래스 하게 찾는다.
* 프로삭이 완전히 실패하는 케이스도 기존의 란삭의 성능에 수렴함. - 성능이 무조건 좋을 수 밖에 없음.
---
* PROSAC 알고리즘
* 2개의 이미지가 있으면 distance matching 수행, 매치마다 distance 값을 기록
* 매치된 값들을 담은 벡터가 있으면 오름차순 정렬
* PROSAC에서 몇개 까지 검사할 지 pool size를 정해줌.
* RANSAC 과정 수행. (여기서, 낮은 값이 나오면 search pool을 늘려줌)
* 5개 ~ 10개 정도에서 찾는 경우가 많다.
---
* Lo-RANSAC
* 이 또한, 데이터 패턴을 잘 활용한 예시임.
* inlier 끼리 뭉쳐있고, outlier는 상대적으로 떨어져 있는 경우가 많았음.
* 이 점을 잘 이용 하였음. 정답은 근처에 있고, 랜덤한 위치로 이동 할 필요가 없다는 점을 사용.
* 한 번 루프에 작은 inner RANSAC을 해서 더욱 정확한 값을 얻으려고 함.
* optimization이 되니, 정답에 가까울 수 밖에 없음. - cost find approch
---
* Lo-RANSAC 알고리즘
* 기존의 RANSAC과 동일한 minimal-set-data 설정
* 모델 추론 - 모델 스코어가 너무 적으면 끝내고 바로 재시작
* 성적이 좋으면 새로운 내부 RANSAC을 실행함. 
* 평가 했을 때, inlier라고 판단되는 데이터를 새로운 데이터 셋으로 다루면서 새로운 RANSAC을 함.
* inlier로 하다보니 더 좋은 결과가 나올 수 밖에 없음. (가우스-뉴턴, 레벤버그 마르카르트 최적화 알고리즘 사용 해서 정답을 최적화)
* 계속 반복























