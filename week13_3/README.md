# 강의 요약
## Least squares - 최소자승법
* 다시 SLAM의 정의로.. - 동시적 위치 추정 지도 작성 (기존의 로컬라이제이션, 매핑 기술과 다르게 최적의 값을 두가지를 동시에 계산)
* 최적화 - 방정식에서 완벽하게 떨어지는 값을 찾지 못할 때, 가장 적은 에러를 가지는 값을 찾는 수학적 기법.
* 최소자승법은 SLAM에서 사용할 최적화 방법.
* 에러 값을 제곱하여 에러로 취급함. 비교적 높은 값을 가지는 에러는 더 큰 에러를 가지게 됨.
* 제곱값이 최소 값이 되는 방법을 이용함.
* over-determined system임. - 미지수의 개수보다 방정식의 개수가 많음.
* 왜냐하면, 풀려고 하는 state의 개수보다(랜드마크의 수, 카메라 pose) 센서 데이터가 더 많기 때문이다.
* x = state, z = 센서 값, f(x) = state를 통해서 추정된 z가 나오는 수식, z^ = 추정된 센서 값
* z와 z^의 값은 차이가 있음. - 모델링 에러 및 노이즈때문에. -> 해당 차이가 에러라고 볼 수 있음.
* 모든 에러의 값들의 합이 최소화가 되는 x의 값이 무엇인지 찾는 것이다.

![image](https://user-images.githubusercontent.com/55529455/171386839-f0f7d3a4-bc90-49df-bb28-dcf6cf11920f.png)


## Maximum-a-posteriori (MAP) estimation in SLAM - 최대사후확률이 슬램에 어떻게 적용?
* sensor measurment 2가지
* proprioceptive senseing, Exteroceptive sensing
---
* proprioceptive senseing
* x(k-1) - 이전 프레임의 상태
* uk - 컨트롤, 오도메트리(이전 상태와 현재 상태의 위치 차이) - 컨트롤의 경우, 제어의 관점으로 전방으로 5m 측량관점의 경우, 오도메트리 센서가 5m 움직였다고 했을때
* eu - 모션 노이즈 (노이즈라고 보면 됨.)
* 현재 프레임의 상태는 이전 프레임의 상태에서 이동치를 더하고, 노이즈를 더한 것.

![image](https://user-images.githubusercontent.com/55529455/171389516-df0ed770-cc45-48e5-adfd-b0683a9582d0.png)

---
* Exteroceptive sensing
* 랜드마크에 위치에 관한 상태를 추정할 수 있는 수식
* xk - 현재 로봇의 상태
* li - 랜드마크들의 상대적인 위치
* ez - 노이즈
* distance는 간단하게 피타고라스 정리로 풀어냄.
* bearing은 x값 y값의 거리를 구하고, 아크탄젠트로 방향을 구함. 현재 방향의 각도를 빼줌 로봇과 랜드마크의 상대적인 변화를 구함.

![image](https://user-images.githubusercontent.com/55529455/171390031-1588bbc6-55aa-415a-8e94-041947e33933.png)

---
* 한개의 모션 상태와 다수의 랜드마크 상태가 출력
* 시간이 지나면서 움직이면서 pose가 바뀌고, 랜드마크의 관측값도 바뀜. - SLAM state가 더 생김
* 잘 분석해서 로봇 pose와 랜드마크 상태를 구하는것이 SLAM

![image](https://user-images.githubusercontent.com/55529455/171390601-8ca1b833-a128-4989-8dc2-d26dab3eb8b6.png)

* 어쩔 수 없이 시간이 지날수록 노이즈가 쌓임.
* 이를 해결하기 위해서 루프 클로저 알고리즘을 사용함.
* 노이즈 패턴을 분석하면서 가장 최적의 랜드위치 값, 로봇 pose 값을 찾으려 한다.
* 이를 통계적으로 얘기하면, belief라고 함.
* 과거의 통계는 어떠고, 최적의 파라메터가 무엇이 되어야 최적의 값인지 유추하는 것.
* 로봇 pose, 랜드마크위치 값은 사후 데이터이기 때문에, 최대 사후 확률을 구하는 문제를 풀게 되는 것이다.
* MAT를 풀기위해서는 모션, 옵서베이션 모델의 확률 분포를 잡고 확률 분포를 정확하게 표현하는 상태를 찾는 것이 목적
---
![image](https://user-images.githubusercontent.com/55529455/171399611-27667706-061b-42ce-97a3-70c1477afbc0.png)
* 0에 수렴한다고 생각 할 때, 노이즈가 없다고 생각하게 됨. 이를 왼쪽으로 옮긴다.
* 다른 해석으로 보면, xk - f(xk-1, uk)가 e와 동일하게 되는 것이다 라고 볼 수 있다.
* 마찬가지로 아래내용도 비슷하게 됨.
* 왼쪽 시그마 - 모델 에러값, 오른쪽 시그마 - 옵서베이션 에러값
---
* 모델 에러값만 최적화 했을 때, 이를 통해서 tansepose를 그릴 수 있게 됨.
* 각각 로봇 pose의 옵서베이션을 보고 랜드마크 위치를 그리면 서로 동일하지 못하는 상황이 나옴.
* 로컬라이제이션하는데 맵이 부족하거나 매핑하는데 모션이 부족하면 이러한 그림이 나오기도 함.
![image](https://user-images.githubusercontent.com/55529455/171399766-f28056ef-6053-498a-bd32-dbd9a261b493.png)
* 모델에러 + 옵서베이션 에러값을 최적화 했을 때, 다음과 같은 그림이 됨.
* 최소화된 에러를 가지는 파라메터 (상태)를 계산함.
* 여러개의 함수를 한번에 최적화 해서 상태를 구하는것을 조인트 옵티마이제이션이라고 함.
* 여기서 SLAM의 핵심이 나온다. - 동시적 위치추정 및 지도 작성
![image](https://user-images.githubusercontent.com/55529455/171399950-51a52594-00a1-40f8-be94-6aec5afc2a5a.png)

## Graph-based SLAM - 그래프 기반 슬램
* SLAM의 2가지 방법
* 1. Incremental SLAM - 필터 기반 알고리즘 사용, 파티클 필터, 익스텐드 칼만 필터
* 2. Batch SLAM - 오프라인 슬램이라고도 함. 그래프 최적화 알고리즘.
---
* Incremental SLAM은 가장 최종의 상태만 추정하는 것이 특징임.
* 이전 상태의 정보는 새로운 정보에 영향을 준다.
* 이전의 상태, 컨트롤 입력, 옵서베이션 정보만 있어도 되므로 빠르게 계산이 되는 장점이 있음.
* 최신 정보를 주기 때문에 과거에는 실시간 사용가능하므로 온라인 SLAM이라고도 함.

![image](https://user-images.githubusercontent.com/55529455/171407945-a55c0f98-8b12-4277-8c61-d8ef0b0a2db7.png)

---
* Batch SLAM - 여러시점의 상태를 한꺼번에 추론함.
* 동시에 여러 정보를 독립적으로 추론하기 때문에, 드리프트 에러는 잘 해결됨.
* 하지만, 그만큼 많은 정보를 하므로 계산량이 많아짐.
* 실시간 처리가 불가능하다는 의미로 오프라인 SLAM이라고도 불림.
* 요즘은 방법을 이용해 온라인에서도 사용가능.

![image](https://user-images.githubusercontent.com/55529455/171408291-aba02dce-28d5-4829-aa9d-804cd52b0581.png)

---
* Incremental SLAM은 빠르지만, Batch SLAM보다 부정확하다.
* 2012년에 발표한 V-SLAM by filter에 따르면, 동일한 계산을 수행한다면, Batch SLAM이 Incremental SLAM보다 더 정확하다는 논문이 나옴.
* 그 후로, V-SLAM은 Batch SLAM 방식을 사용하게 됨.
* 현재로서는 Factor SLAM으로 이루어지게 되었음.
* Factor SLAM은 노드와 그래프로 이루어진 SLAM
* 노드에는 로봇 state, 랜드마크 state 저장
* 엣지에는 모션, 옵서베이션 정보가 저장됨. (Factor)
* 그래프를 최적? - 모션 모델과 옵서베이션 모델을 이용하여 최적화 한다는 것 - 직관적 구조로 SLAM에서 가장 유명한 그래프 표현 방식
---
* 그래프로 표현됨으로써 - 엣지를 통해 모션, 옵서베이션 링크를 쉽게 파악을 할 수 있게 됨.
* 이를 이용해서 그래프 루프가 생긴 경우, 그래프 최적화를 통해서 누적된 언설턴티를 제거해주고, 루프 안에 노드들에 대한 포즈와 랜드마크포즈의 최적값을 찾을 수 있게 됨.
* 루프 클로저 기술로 인해서 테이블이나 방에서 사용할 수 있었던 기술이 매우 크게 볼 수 있게 됨. (노이즈를 쉽게 잡을 수 있게 됨)
* SLAM에서도 파이프라인이 생김. - 프론트엔드에서는 그래프의 노드와 엣지를 추가해주는 작업, 백엔드 - 루프클로저가 생기거나 트리거가 되는 그래픽 최적화 알고리즘 수행
* V-odometry - 누적된 드리프트를 제거 할 수 있는 방법, 글로벌 스케일로서 그래프 옵티마이저가 불가능
* V-SLAM - 반대로 있다.

## Bundle Adjustment
* 2-view 지오메트리를 사용하면서 2d-2d correspondences가 있고 이를 통해 E-matrix, F-matrix를 구해서 두 이미지의 R,T를 사전에 구함
* 그걸 이용해서 3D 랜드마크 포지션을 구함.
* Bundle Adjustment는 한단계 더 나아감.
* n-View가 된다. R과 T 값을 가지고 있다.
* 2d-2d correspondences가 있고 3D 랜드마크 포지션도 다 알려져있음. 하나의 랜드마크에 2개 이상의 correspondences가 생겨있다.
* 모든 것을 다 계산 해놓은거 같지만, 로봇이 이동하면서 모션에 옵서베이션 노이즈가 프레임마다 생긴다. - 다 실제로 정확한 값이 아님.
* 그렇기 때문에 이를 해결하기 위해서 batch SLAM 기법을 사용함. 2d-2d correspondences, 2d-3d correspondences, 모션을 이용해서 카메라 pose와 3d 랜드마크 위치를 보정
* 보정을 한다? - 그래프 최적화를 통해 uncertainty(불확실성, 언설턴티)를 해결해준다.
* 지난 강의에서 모션의 e와 옵서베이션 e 값이 필요하다고 했음 - 하나의 cost function으로 표현 가능함. - reprojection error
* 3d 랜드마크와 카메라 pose가 완벽하게 일치했을 때, 이미지 플레인에 투영했을 때, 피쳐가 뽑힌 위치로 투영이 됨.
* 하지만, 노이즈가 있기 때문에 항상 오차가 나타남. - 이를 재투영 에러라고 함.
* 에러값을 줄이기 위해서 랜드마크가 키포인트 쪽으로 이동하느냐, 랜드마크가 고정이고, 카메라가 이동해서 ray로 가까이 가느냐로 해결.
* total 재투영 에러를 줄이기 위해서는 최적의 카메라 위치와 최적의 랜드마크 위치를 찾는 것이라고 본다.
* 선형적이지 않기 때문에 최적화 수식을 쓸 때, 미분으로 할 수가 없다.
* 그렇기 때문에 비선형 최적화를 사용해야한다.
* 비선형 공간을 어떻게 선형으로 바꾸어서 근사화 시켜 최적의 값으로 유추하는지? - 가우스 뉴턴 방식이 있음.
---
* Bundle Adjustment가 어떻게 사용되는가? 
* 1. 루프 클로저를 수행할 때
* factor 그래프에서 루프가 발생하면, 루프와 옵서베이션을 최소화 시켜줄 수 있음.
* 2. sliding-window optimization 기법 사용
* 그래프 최적화 하지만, 실시간으로 좋은 pose 추정할라는 알고리즘이 있다.
---

## Nonlinear optimization
* 3d 랜드마크 위치 (Xi, Yi, Zi, 1)
* 카메라의 회전, 이동 행렬 R, T
* 카메라 내부 행렬 fx,fy,cx,cy,s - 모노 카메라를 쓴다면, 계산에서 제외됨. 다양한 카메라로 찍었을 때, 계산이 가능하게 만들었다.

![image](https://user-images.githubusercontent.com/55529455/171414337-7501be89-5ffb-4a31-9b8f-66a0d2e07c94.png)
![image](https://user-images.githubusercontent.com/55529455/171414832-09a5c536-148d-4911-9254-2990b4c0cdda.png)

---
* BA 최적화 문제는 최종 재투영 에러의 최소값을 가지는 상태는 어떤 pose인가?
* 이문제를 풀기 위해서 최소자승법을 사용. 단, 가우시안 분포도를 사용한다는 전제가 깔림.
* 가우시안을 사용하는 이유? - 가우시안 데이터를 사용할 때, 최소자승법이 Maximum Likelihood Estimation (MLE) 문제로 수렴됨.
* MLE 문제는 통계적으로 해결 했을 때, 수식적으로 최적값을 가진다는 것이 보증되어있음.
* MLE 문제를 푸는 것이 다른 방법에 비해 간단하기 때문이다.
* 위의 식에서 가우시안이 추가가 된다.
* 2번째 사진 E(x)은 1번째 사진의 결과값이다.
* 델타x로 바뀌기 때문에, 안의 값도 델타 x의 값으로 바꿔서 식을 변형함.
* 3번째 사진은 비선형적인 식을 미분하여 선형적으로 바꿔주는 것이다.
* 테일러 공식을 이용하여 1차 미분에 대한 근사값을 얻을 수 있음.
* Ji - 자코비안 (1차 미분값 매트릭스)
* 4번째 사진은 1차 미분한 값을 가져온 사진이다.
* 2차 방정식으로 정리가 된다.
* 2차 방정식은 최소값, 최대값이 나오게 된다. - 이를 델타x에 대해 1차 미분해주면 5번째 사진이 된다.
* 무슨뜻이냐? x0 시작값에서 1차 미분하면 근사 2차 방정식이 나옴.
* 2차 방정식의 나온 값의 최소값이 나오면 옵티멀하다고 생각한다. - 글로벌 옵티멀하지 않음, 근사값이기 때문. 가깝다고만 생각함.
* x0과 x1의 이동치를 구했다고 생각함. 이 과정을 반복함으로써 x2를 구하고, x1과 x2의 이동치를 구하고... 점진적으로 솔루션에 가까워짐.
* 이를 인터렉티브 옵티마이제이션이라고 함.

![image](https://user-images.githubusercontent.com/55529455/171416376-f60ba28e-d234-4c93-b85b-a9e4f5df42d0.png)
![image](https://user-images.githubusercontent.com/55529455/171416680-8e852d30-e32b-480b-9f75-18e25c5bc408.png)
![image](https://user-images.githubusercontent.com/55529455/171416739-6252b78c-a2f2-43cc-b2c7-6bf0f7606ce2.png)
![image](https://user-images.githubusercontent.com/55529455/171417045-28be8e2a-10b8-46aa-b08a-cf407666d24b.png)
![image](https://user-images.githubusercontent.com/55529455/171417240-506c399b-2e19-425f-88f4-008e99bd08ae.png)

---
* 굉장히 어려움!
* H 행렬 크기가 매우 큼.
* 예시 사진. - 2만개의 사진, 18개의 이미지 포인트
* 보통의 방법으로는 구하기 힘든 행렬임. - VSLAM은 1천개 이미지 뽑고, 이미지 포인트가 100개가 넘어감..!!

![image](https://user-images.githubusercontent.com/55529455/171418237-d60ebd0f-85ca-480e-8bb7-9d2d6701d48c.png)

---
* 자코비안 매트릭스는 대부분 매트릭스가 비어있다는 점을 알 수 있다.
* factor마다 연결성을 미분한 매트릭스인데, 노드들은 인접한 정보는 연결되어있지만, 멀리떨어져있으면 연결이 안되어있음 (x1, x3의 관계)
* 이러한 매트릭스를 Sparse 매트릭스라고 함.
* b 매트릭스 또한 많이 비어 있음! - 자코비안 매트릭스가 비어있기 때문에.
* H 매트릭스 역시 많이 비어 있다. - 이 또한 같은 이유
* Sparse 쓰는 방법이 좋은 방법은 아님.
* Schur Complement 방법이 있음.

![image](https://user-images.githubusercontent.com/55529455/171418496-b8efed82-2f98-4066-bb31-9b884a867999.png)
![image](https://user-images.githubusercontent.com/55529455/171418873-406257cf-7306-4844-8ef9-f4e2a67eb82f.png)
![image](https://user-images.githubusercontent.com/55529455/171418986-3edbbfe7-193f-43cb-8623-4a9f84732fbd.png)
![image](https://user-images.githubusercontent.com/55529455/171420447-7a3ed25a-9ce2-4c60-9745-b547667803b0.png)
![image](https://user-images.githubusercontent.com/55529455/171420523-b4dcce77-c2d2-46f0-aefc-9cc959c9f607.png)

---
* Schur Complement
* Hs(B) 랜드마크의 x, y, z location에 대한 정보가 올라와 있음
* Hc(C) 카메라 pose의 x, y, z의 정보가 올라와 있음.
* Hs가 적은 이유는 로봇이 움직여도 동일한 포인트를 보고 있을 확률이 높아서 파라메터가 작음.
* Hsc는 옵서베이션의 식에 대한 정보
* 이 식을 풀기 위해서 양쪽 변에 2번째 사진 중앙에 있는 행렬을 곱함.
* 델타 c만으로 아래 식을 구할 수 있다. - Schur Complement 식이라고 함.
* 이미 다 있는 데이터이기 때문에 가져오면 됨. 하지만, Hs의 역행렬을 구해야함.
* 역행렬 구하기는 쉬움. 생각보다 빠름.
* 역행렬을 구하고 나면, Ax = b 형태로 나타남. Schur Complement 부분이 A가 됨.
* 하지만, Ax = b 를 x = A^-1b 형태의 역행렬로 하기가 큼.
* 일일히 하나씩 역행렬 해주기 어렵기 때문에, 행렬 계산을 해서 하나의 큰 행렬로 만들어서 역행렬을 쉽게 할 수 있는 행렬로 분해할 예정.
* LU decomposition을 사용함.
* 델타C를 구했으니, 델타S를 구하면 됨. 델타C - 카메라 파라메터가 어떻게 바뀌어야 델타s를 가지냐?
* 델타S는 3D 랜드마크 포지션이 델타x의 입장에서 파라메터가 얼마나 바뀌어야하는가?

![image](https://user-images.githubusercontent.com/55529455/171421180-97dabbca-a667-4326-823a-87735782aaed.png)
![image](https://user-images.githubusercontent.com/55529455/171421926-a94c86dc-dd16-47c0-a4a5-b34a5f40ef32.png)
![image](https://user-images.githubusercontent.com/55529455/171422614-4160d067-7dde-44f1-980f-affd63bc1da8.png)
![image](https://user-images.githubusercontent.com/55529455/171422801-64e48cc3-62c4-4a4c-8f6b-0081af451d4e.png)

---
* 최소자승법을 할때 주의해야할 점
* 최승자승법이 outlier에 매우 취약한 방법임.
* MSE 커널을 사용해서 데이터 분포를 벗어나는 outlier를 옵티마이제이션 식에서 제외하는 방법을 사용해야함.
---
* 이 방법을 사용 할 수 있는 라이브러리
* Google Ceres-solver
* G2o
* GTSAM















