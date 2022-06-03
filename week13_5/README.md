# 강의 요약 - ProSLAM

* 프로슬램은 가벼운 스테레오 비쥬얼 슬램 알고리즘. 시스템 정리가 잘 되어있음.
* 학생들에게 SLAM을 가르치기에 좋은 오픈소스가 없었다.
* 프로그램이 개념을 잘잡아주면서 논문과 매칭이 잘 되지 않는 SLAM이 많았다.
* 잘 이해 할 수 있는 SLAM을 코드로 옮겼다.
* 모듈러하다. 쓰기도 쉽고 이해하기도 쉬움
* C++ 용어 사용, 외부 라이브러리는 최소화, 오픈소스다

## Introduction
* SLAM은 연구가 많이 된 분야다. 학생과 연구자들이 배우고 있음.
* ORB-SLAM2과 LSD-SLAM가 양대산맥을 이루고 있다.
* 시스템이 고도화 될수록 SLAM이 어려워지고 있음. - 복잡해지고 있기 때문에 점점 이해하기 어려워지고 입문자에게 어렵다.
* 완벽하게 돌아가는 스테레오 비쥬얼 슬램이다. 캡슐화(모듈을 사용할 때, 필요한 기능만 노출) 깔끔한 인터페이스
* 아이겐, 오픈CV, g2o 라이브러리 사용 
* 스테레오 비쥬얼 슬램을 만들었는데, 모노큘러가 더 어렵다. - 초기 맵 만들기 어렵다. 추정을 꼭 해야하는 점이 있다.
* 모노큘러의 단점은 스케일 드리프트가 발생하게 됨. - 스케일을 추정 할 수 없고, up-to 스케일로 추정함. (스케일 드리프트 = 스케일 오차)
* 이전 프레임 스케일과 현재 프레임 스케일이 동일한 스케일로 유지되어야 하는데, 안되는 경우.
* 스테레오 비쥬얼 슬램만 공부해도 슬램에 관심을 유도하기 충분하다.
* stereo rectification = epipolar할때, 전방 스테레오 카메라인 경우, lotation없고, trans 만 있을 때, (epipolar line이 row만 나올때)
* 거친 스테레오 이미지 (rectified), 디스토션이 풀어짐. (undistorted)
* 센서의 대한 깊은 이해에 필요한 부분은 프로그래머가 알기 힘듬 - 물리학적인 부분이기 때문.
* feature based를 사용함. - 전방 스테레오 카메라를 쓰기 때문에, epipolar geometry를 정확히 알기 떄문에, 3D corresponding point를 알기 쉽다.
* 트래킹 되고 있는 이미지 포인트로 랜드마크를 만들고, salient points로 랜드마크를 사용한다. (3D에서)
* trajectory(카메라 이동경로)에서 작은 부분에서 보였던 랜드마크를 작은 포인트 클라우드를 만들것이다. (local map을 만들것이다. - 국소적인 맵) (global map - 전체맵)
* pose graph (== factor map)
* deformable하다 - 형태가 바뀔 수 있다. ㅎ모그래피에서 형태가 바뀐다? 랜드마크의 위치가 바뀌거나 카메라 위치가 바뀌거나. 즉, 그래프 최적화를 통해 (bundle adjustment)
* spatial backbone (공간적인 백본(바닥) == 결국 factor graph)가 deformable, local map도 deformable 할 수 있다.
* robot revisits a known location (루프 클로저를 수행 했다는 뜻. re-visit) - 이러한 최적화로 인해서 deformable 할 수 있는 것.
* 병렬처리화 시킬 수 있었지만, 그럼에도 (성능을 높일 수 있었지만) 병렬처리의 메모리 관리, 쓰레드 동기화로 인해서 싱글 스레드로 다 끝냈다. 구현이 쉽고, 디버깅도 쉬움.
* 병렬처리가 없어도, 정확도가 state of art algorithm과 같다. 계산량이 적다.

## Related Work
* large-scale(건물, 도시) 에서 돌 수 있는 슬램을 소개
* 어떤 점이 비슷하고 다른지 설명한다.
* FrameSLAM이 있는데, bundle adjustment를 실시간에 돌릴 수 있고, censure, IMU를 사용한다.
* S-PTAM(PTAM의 스테레오버전)은 2개 스레드에서 돌고, brief feature을 사용함. g2o 라이브러리로 풀 번들 에드저스트먼트 가능.
* ORB-SLAM2는 엄청 좋은 정확도를 가지고, ORB feature를 사용해서 relocalization을 빠르게 수행함. ProSLAM에서 사용하는 랜드마크 지정등이 잘 들어가 있음.
* ORB-SLAM2는 실시간으로 가능하다. (bag-of-words 사용), g2o를 사용해서 local bundle adjustment 함. 3개의 병렬 스레드 사용
* LSD-SLAM은 direct featureless 방식, large-scale 잘 돌고, 빠르고, 싱글 스레드 사용함.

## Our Approach
* ProSLAM은 3D map을 만드는 것을 목표로 함.
* 3D 맵은 로봇이 보고 있는 맵, 랜드마크로 이루어져 있다. - 3D 세상에서 salient point다.
* 랜드마크 주변은 local-map이라고 한다. - 하나의 랜드마크는 여러개의 디스크립터의 정보가 있다. (이전 로봇pose, 이후 로봇pose도 해당 랜드마크를 볼 수 있다면 데이터가 담김)
* factor graph 방식을 사용함. (pose graph)
* 3D isometry (4x4, R, T) (== SE3)매트릭스를 담고 있다.
* 로컬맵들이 점점 이어지는 스페셜 constraint가 있다. - 카메라 모션을 트래킹 해서 생긴다. - re-localization 이벤트일때, (루프 클로저가 실행) 이전 맵을 보정하여 이어줌
* SLAM map이 하는 목적이 무엇이냐?
* 1. Relocalization
* 2. Adjustment
* Relocalization은 현재 보고 있는 로컬맵과 기존의 로컬맵과 비교해서 디스크립터가 비슷하면 Relocalization.
* bundle Adjustment 해주기 위해서 그래프 최적화 할 때, factor graph를 가지고 있기 때문에, g2o 라이브러리로 할 수 있다.
* 로컬맵으로 한다면, 작게 잘라진 맵에서 일부만 봄으로써 size of adjustment를 할 수 있다.
* 글로벌 맵으로 본다면, full bundle Adjustment인데, 이는 무겁다. - 로컬맵을 사용하니깐 쉽게 할 수 있다. 계산량이 적어짐. full보다는 정확도는 낮다.
* 그럼에도 불과하고 결과는 괜찮다!
* 로컬맵을 만드는 과정 - 4개의 분리되어있는 모듈로 작성됨.
* 1. Triangulation - 스테레오 페어 이미지를 받아서 랜드마크를 만들어주고, 랜드마크에 왼쪽 오른쪽 이미지에서 보였던 디스크립터를 달아준다.
* 2. Incremental Motion Estimation - 2개의 이미지 사이에서 모션을 구하는 것.
* 3. Map Management - 로컬맵을 확장시켜주면서 랜드마크 포지션을 보정해준다.
* 4. Relocalization

![image](https://user-images.githubusercontent.com/55529455/171805498-455d1157-0b7e-422e-accd-842263758524.png)

---
* 중요한 데이터 구조가 어떻게 되어있는가에 대해서 알려줌.
* rectified, undistored된 이미지 데이터만 담는다. - 2D array 이미지로 들어온다. (값은 픽셀의 밝기값)
* r, c = row,col (integer로 받을 수 있다.
* r, c를 통해서 이미지 코디네이터를 표현함.

![image](https://user-images.githubusercontent.com/55529455/171805754-508decc7-90a7-4895-98d0-1a7983308380.png)

---
* 키포인트와 디스크립터에 대한 정보
* responce - ORB feature 같은 경우, 해리스 코너의 corner core-ness score
* keypointWD (keypoint with Descripter)
* r, c = 키포인트 위치, response, descripter는 디스크립터 단계에서 뽑는 것. 

![image](https://user-images.githubusercontent.com/55529455/171805988-59b34abb-0c7e-4dcf-aef9-aa2ce1e6543f.png)

---
* epipolar 과정 - framepoint에 저장함.
* k_l, k_r = 왼쪽 오른쪽 카메라 키포인트
* p_c = x, y, z 카메라 코디네이터
* p_w = x, y, z 월드 코디네이터
* prev, next = 다른 프레임포인트로 이동이 가능.
* landmark = 랜드마크
* inlier = 좋은 데이터인지? 검사

![image](https://user-images.githubusercontent.com/55529455/171807512-e3f88a10-acea-48e6-92e2-9f539c3c5f1c.png)

---
* 프레임포인트를 이전과 현재 포인트 비교 할 때, (왼쪽 오른쪽 둘 다 매칭이 됐을 때, 확실한 피쳐가 있을 때) 3D에서 어떤 위치에 있는 지 알 수 있다.
* 매칭이 됐다면, 이전 프레임을 prev에 연결해준다. prev 가 있다는 것은 이전에 보였던 프에임 포인트가 지금도 보이고 있다. - 계속 같은걸 보고 있다.
* 시점에 따라서 보고 있으므로 맵을 바라보고 있는 정보를 이용해서 프레임과 프레임 사이의 모션을 구할 수 있다.
* Trangulation module - 왼쪽 오른쪽 둘 다 봤을 때, 몇천개의 피쳐를 뽑음. 매칭을 했을 때도 몇천개가 있음. (좋은 피쳐인지는 모르겠지만)
* 프레임포인트가 많아질 수 밖에 없다.
* c2w, w2c - 카메라, 월드 좌표계의 위치 표현 (translation)
* points[] - 굉장히 많음 프레임포인트
* Camera - 아마도 instric, extric
* Frame이 10mb라면..? 엄청 크다;; 아마 잠깐동안 가지겠지..
* 월드 코디네이터 기준으로 카메라 코디네이터를 표현한다

![image](https://user-images.githubusercontent.com/55529455/171813920-fc001d48-a295-494d-ba7f-7ae10d28857f.png)

---
* 랜드마크 표현
* p_w - 월드 코디네이터 기준 랜드마크 x, y, z
* origin - 어떤 프레임이 표현하는 랜드마크인가?
* omega - BA 할때, 리스트 스퀘어 문제를 풀기 위해 가우시안 노이즈를 선정했을 때, x 트랜스포즈의 정보 매트릭스 * 에러식을 표현한 것. (3x3)
* nu - 랜드마크의 위치를 최적화 시켜주는 과정에서 인포메이션 필터의 정보를 가지고 있다.
* p_w를 통해서 현재 위치를 표현 가능
* origin을 사용해서 랜드마크의 프레임포인트로 링크 가능 - 그 프레임으로 갔을 때, prev, next를 갈 수 있다.

![image](https://user-images.githubusercontent.com/55529455/171814354-bc9daac7-aa92-4c54-a738-f5ccc4e6c55a.png)

---
* 로컬맵, 글로벌맵 표현
* 여러개의 프레임, 랜드마크 가지고있고, 로컬맵의 중심에서의 트랜스포즈를 가지고 있다.
* 여러개의 맵, 랜드마크, g2o, 글로벌맵 중심의 트랜스포즈 가짐.

![image](https://user-images.githubusercontent.com/55529455/171815292-b1b5d118-197d-41ed-81e8-4973b16c1c81.png)
![image](https://user-images.githubusercontent.com/55529455/171815311-5c1cdb82-25bc-4a45-935d-d591c8b194c2.png)

---
* Triangulation
* 스탠다드 핀홀 카메라 사용
* 가장 처음으로 feature detection 해서 k_l, k_r을 출력하는데, FAST keypoint 디텍터를 사용함.
* 적정량의 키포인트를 뽑기 위해서 실시간으로 FAST 임계값을 뽑음.
* 한쪽에 패스트 코너가 쏠려있으면 정확한 epipolar 정보를 뽑을 수 없음. - 이미지 전체에서 FAST 뽑을 수 있도록 함. (regularization)
* 이미지를 bin으로 쪼개서 bin들마다 최소 몇개씩 뽑혀야 한다고 기재
* 특정 bin에서 가장 높은 response를 가지는건 남기고 나머지는 버린다. (가장 코너 같은거만 남겨놓는다.)
* 이렇게 하면, 왼쪽 raw 이미지에서 엄청 많은 키포인트가 뽑히게 되지만, 중요한 것만 남기고 다 버리게 됨.
* 오른쪽 이미지에서는 하지 않음. 오른쪽 좋은 피쳐와 왼쪽의 좋은 피쳐가 매칭 된다는 보장이 없음. - RANSAC 같은 걸 써서 좋은 매칭이 되도록 희망.
* 스탠다드 BRIEF 디스크립터를 뽑음. 실시간에 쓰기 좋다.
* 그 다음에 epipolar를 뽑음.
---
* 코드해석
* 왼쪽, 오른쪽 키포인트 뽑음.
* 비어있는 배열을 만듬.
* sort를 통해 높은 response 순으로 정렬
* 모든 왼쪽에 있는 키포인트 루프
* * 왼쪽에 있는 데이터 오른쪽과 왼쪽에 있는 데이터를 왔다 갔다 하면서 찾음. - (오른쪽 키포인트가 왼쪽것보다 낮으면 - 왼쪽 스킵)
* * bookkeeping - epipolar와 유사함.
* * 왼쪽 키포인트 루프
* * * 왼쪽에 있는 키포인트와 오른쪽 이미지에서 똑같은 raw search하면 하는가? 완전 동일한 픽셀에 있다면 패널티가 없으므로 잘못된 데이터라고 판단함.
* * * 아니면, 최적의 distance를 계산함. (적은 distance) - 해밍 디스턴스 사용.
* * 괜찮은게 나왔으면 매치라고 하는 것이다.

![image](https://user-images.githubusercontent.com/55529455/171816376-a463e0ab-2d52-4a2b-b2c1-ee9070866f1d.png)

---
* 디스크립트 기반으로 depth를 얻음. (p_c.z = B / (k_R.c - k_L.c))
* depth를 구하면, x와 y도 구한다.
* p_c.x = p_c.z/F_x * (k_L.c - C.x)
* p_c.y = p_c.z/F_y * (k_L.r - C.y)
* 이렇게 구한 p_c를 framepoint P에 저장함.

![image](https://user-images.githubusercontent.com/55529455/171818118-23ecbc67-b845-4fe8-8cae-b459c4dd833c.png)

---
* Motion Estimation module의 목적
* 왼쪽 카메라가 어떤 모션을 가지는가? F(t-1)과 F(t)의 상대적이 모션이 어떠한 값을 가지는가?
* F(t)와 F(t-1)을 연결 시켜줄 수 있다면, 실제 3D 랜드마크를 트래킹을 한다면?
* 2 프레임 사이에 상대적인 모션을 계산 가능하다. - 새 프레임의 c2w를 얻을 수 있다. (이전의 글로벌 포즈에 상대적인 모션을 더하면 됨.)
* Tracking unit이 따로 있음. - 이를 통해서 framepoint의 correspondences를 구할 수 있음.
* 왼쪽 카메라에서만 대해 모너큘러 트래킹을 한다는 것. 피쳐 포인트, 매칭 성공한것만 남았기 때문에.
* 이전 프레임의 포인트를 현재 이미지에 올려야 함. - 이전 프레임 포인트를 현재 포인트에 재투영 한다는 것이다.
* k_P = pi(P_L * w2c * p(t-1).p_w)
* pi(p_w) - 카메라 프로젝션 함수.
* k_P를 구하고 나면, 이전 프레임 포인트를 새로운 이미지에 투영을 시켜 하나의 키 포인트가 되는 것인데, 디스크립터도 가지고 있음.
* 이를 constant velocity motion 모델을 사용하여 위치를 추정할 수 있다.
* 재투영된 k_P를 실제 현재 프레임 피쳐와 매칭을 시켜서 correspondense를 추정. - 여기서는 k_P에서 가장 가까운 키포인트 k_L을 찾음.
* 닮았으면, 이것을 가지고 Pose optimization을 수행. - pose prior w2c를 가 있고, 이를 가지고 키포인트 매칭을 통해서 reprojection 에러를 최소화하는 pose 구하기 가능.

![image](https://user-images.githubusercontent.com/55529455/171819834-1cb029b4-1f03-42e1-92be-646761282b64.png)


---
* 코드 해석
* 현재 프레임에서 필요한 정보 선언.
* least squares 변수를 만들어줌.
* 모든 프레임포인트 루프
* * 프로젝션을 해서 k_P를 만들어주고, 프로젝션을 왼쪽이미지에 해주고 나서 reprojection 에러를 구함.
* * 그것을 squared error를 구해주고, outlier를 제거해주는 robust kernel 커널을 이용함.
* * 자코비안으로 바꿔주고, 오메가를 업데이트 해줌.
* * H, B 매트릭스 만들어주고
* x값을 얻는다. - 미분이 가능하게 한 pose를 가지게 됨. - 이를 3x3으로 돌려서 w2c, c2w를 구함.

![image](https://user-images.githubusercontent.com/55529455/171819947-c962597b-a2ba-4c69-915e-118efe4d4d99.png)
![image](https://user-images.githubusercontent.com/55529455/171820154-c575fdec-bd7f-4d11-9fe7-61205a5b3df3.png)
![image](https://user-images.githubusercontent.com/55529455/171820478-65283386-998e-4777-9bec-6ccabd242d76.png)
![image](https://user-images.githubusercontent.com/55529455/171820616-2f7f5650-79d0-4ff4-aae4-d93388c22acd.png)

---
* Map Management
* 3가지의 주요 작업이 있음.
* 1. Correspondence recovery
* 2. Landmark optimization
* 3. Local map generation
* Correspondence recovery - 지난 프레임에 있었던 프레임포인트들이 현재 이미지에서 제대로 트래킹 되고 있는가?
* Motion Estimation에서도 하긴 하는데, constant velocity motion 모델이라 해서 간단히 수식적인 모델을 사용해서 트래킹 유지
* 정확한 값은 아니고, 초기값을 사용함으로써 pose optimization하는게 더 정확하기 때문에, 모든 프레임포인트가 안될 것이라고 가정한 것이다.
* pose optimization 해서 나온 정확한 값을 다시 projection 해줌. 디스크립터 기반으로 다시 매칭 해줌.
* 매칭 거리가 괜찮으면 correspondence라고 만들어줌, 새로운 포인트링크를 만들어 링크해준다.
* 랜드마크를 볼때마다, information 필터를 이용해서 값을 조금 더 보정
* 로컬맵이 생기는 조건 2가지
* 1. 이전의 로컬맵보다 많이 이동했거나
* 2. 이전의 로컬맵보다 더 회전을 했거나
* 로컬맵이 생성되면, 현재 프레임에서 가지고 있는 글로벌 pose를 로컬맵 pose로 지정한다고 함.
* 이전에 만들었던 로컬맵으로부터 모여있던 모든 프레임들과 랜드마크가 새로운 로컬맵에 저장됨.

![image](https://user-images.githubusercontent.com/55529455/171824338-aa9459c3-75a4-4039-a446-39934c9a659a.png)

---
* Relocalization
* 예전에 들려본 장소가 있다면, 이 정보를 사용해서 현재 위치를 조금 더 개선 할 수 있다.
* 가장 이해하기 쉬운 방법으로는 매 프레임과 비교하면 된다.
* 현재 있는 로컬맵을 예전에 있던 로컬맵과 비교한다. - 모든 이미지를 비교하는 것은 아님.
* 랜드마크와 랜드마크 사이의 correspondense를 구해야함.
* 이를 구하기 위해 similarity search를 하는 것은 매우 무겁다. - 계산량 많음.
* 로컬맵끼리 영역이 얼마나 겹치는지 확인한다. 이게 된다면, similarity search 수행. 아니면 안한다.
* HBST 라이브러리를 사용함. - 굉장히 성능이 좋음. 디스크립터 매칭 알고리즘
* 디스크립터 매칭을 수행해주고, 랜드마크끼리 매칭이 됐다면, ICP 사용.
* ICP - 포인트 클라우드 사이에 상대적인 모션이 어떻게 되는지 알아보는 알고리즘.
* 마지막에는 ICP가 끝나면, 초기값으로 상재겅니 모션이 나오면, g2o 라이브러리를 써서 loop optimitzation을 해준다.


