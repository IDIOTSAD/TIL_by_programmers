# 강의 요약

### 소개
* 데이터 탐색에서는 자신이 원하는 데이터가 있는지 확인
* 데이터 가공 단계에서 전처리 과정이 중요함. - 사람이 하는 과정이기 때문에 노이즈가 생길 수 밖에 없음
* 데이터 검증을 통해 올바른 데이터가 있는지 확인
* 데이터 나누기를 통해서 어떤 것을 테스트, 평가, 학습에 쓸 데이터인지 나눠야함.
* 학습 방법 결정을 통해서 어떤 포멧으로 할 지를 결정해야함. - 모델 만들기와 연결됨.
* 모델 검증을 통해 만들 모델을 검증을 해야함.
* 대규모 학습을 통해서 실전을 함. - 녹색부분은 큰 관련은 없음.

![image](https://user-images.githubusercontent.com/55529455/166404113-e04c81ee-490d-4878-9d90-a89b82d5ab63.png)

### KITTI
* 자율주행 데이터는 아니지만, 카메라, 라이다, GPS 등 다양함.
* SLAM을 위한 데이터
* 각 센서와 차량 바퀴의 위치와 좌표계 확인이 필요하다. - 좌표계를 고려하지 않으면, 엉뚱한 데이터가 만들어짐.
* object detection 페이지에서는 2D object, 3D object, bev 시점 객체 인식 데이터 제공
* 스테레오 카메라 구성으로 오른쪽 왼쪽 데이터 얻을 수 있음. 벨로다인 라이다 데이터도 있음.

* 2D object detection 데이터 라벨링 포멧
* 다양하게 구성되어 있지만, type, bbox를 이용할 예정.

![image](https://user-images.githubusercontent.com/55529455/166408405-2ad8c7a6-e6fd-4df0-bcd7-0dcf6a5313c8.png)
![image](https://user-images.githubusercontent.com/55529455/166408505-2873a73f-8416-4246-a124-df60433753d2.png)
![image](https://user-images.githubusercontent.com/55529455/166408652-e6c75878-4a95-4941-ab42-65fb9a5a99d9.png)
![image](https://user-images.githubusercontent.com/55529455/166408813-509aec5b-ca94-4715-b1d8-c1f252b8567b.png)

### BDD100K
* 버클리 대학에서 최근에 나온 (2017) 데이터 셋, 자율주행을 위한 딥러닝 어플리케이션 데이터 셋
* 바운딩 박스보단 세그멘테이션이 더 쉬움. - 세그멘테이션의 min max x, y를 구하면 바운딩 박스로 구현이 가능함.
* KITTI와 다르게 다양한 환경에서의 데이터가 존재함. - 현실적이기 때문에 자율주행에 적합.

![image](https://user-images.githubusercontent.com/55529455/166423096-1e2b0216-33c6-47b6-8b83-fc1821870853.png)
*  json 포멧은 괄호 {} 기준으로 블록을 분할
*  이름 : 값(숫자), 값(문자열) 형식으로 지정함.
*  괄호 \[]은 배열(리스트)를 의미함.

![image](https://user-images.githubusercontent.com/55529455/166423659-2a560b2a-3929-45f4-8dd4-40bfae33068b.png)
![image](https://user-images.githubusercontent.com/55529455/166423876-02dc1844-3c8a-4d38-88bd-6be4c7c2bb32.png)

### Cityscape
* 다양한 도시의 도로 세멘틱 세그멘테이션 데이터
* 세그멘테이션은 객체의 형태를 다각형으로 표현함
* 바운드 박스를 그리기 위해 4개의 포인트가 필요했다면, 다각형은 N개의 포인트를 이용함.

![image](https://user-images.githubusercontent.com/55529455/166425042-850514ee-419d-44dd-95e2-f217d67a008d.png)
![image](https://user-images.githubusercontent.com/55529455/166427869-965f85c1-c43a-4576-9975-88c9b597c930.png)

### 데이터 셋을 찾는 방법
* 실제 풀어야하는 문제에 대해 완벽한 공개 데이터 셋은 존재하지 않음. 자신만의 데이터 셋을 구축하는 것이 필요함.
* 그러나 데이터셋을 구축하는 것은 많은 시간과 비용이 발생하는 작업이기 때문에, 최대한 공개 데이터셋을 활용해야함.
* 데이터셋 구축비용과 유지보수가 힘들기 때문에, 공개 데이터 보고 어떤 규격과 정책으로 데이터를 만드는지 데이터에 대한 지식을 확보하는 것이 중요
* Scale은 자율주행과 관련된 다양한 데이터를 전체적으로 확인할 수 있는 사이트임.
* https://scale.com/open-dataset

### 딥러닝 모델을 찾는 방법
* 딥러닝 분야는 매우 빠르게 발전하고 있어, SOTA(state-of-the-art) 모델이 굉장히 빠른 속도로 갱신되고 있음.
* 다른 특징으로, 논문에 사용된 코드를 공개하는 비율이 높아 다른 사람들이 쉽게 논문에 사용된 모델을 만들 수 있음.
* Papers with code는 코드와 함께 공개한 논문들을 모아둔 사이트로 SOTA 모델을 활용해보기 좋다.
* https://paperswithcode.com





