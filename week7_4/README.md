# 강의 요약

> * linesegmentdetector 함수가 있음. - 허프만보다 속도가 좋은것도 아니고, 정확도가 좋아지는 것도 아님.

> * opencl 의 umat 를 사용하게 되면, opencv를 사용하는 것이 아닌, opencl의 언어로 해석하게 된다.
> * >> 연산을 수행하게 된다면, Mat 형식으로 받은 후, UMat 형태로 변환하게 됨.
> * 만약, umat을 변환 할 때, 간단한 작업만 수행하게 된다면 비효율적임. (Mat -> UMat으로 변환하는데 걸리는 자원이 더 큼)
> * UMat의 결과와 Mat의 결과는 다를 수 있음.
> * 상호 변환 = mat.copyTo, mat.getUmat 함수로 구성됨. (Umat -> mat 동일)

> * OpenCL T-API 사용 시 주의 사항
> * UMat을 사용한다고 항상 좋지는 않음. -> 주로, 영상을 표현하는 Mat에 대해서만 UMat으로 변환 사용
> * Border 처리 연산 시 BORDER_REPLICATE 옵션을 권장
> * Mat::getUMat 또는 UMat::getMat 함수 사용 시 주의 사항
> -> getUMat함수를 통해 UMat 객체를 생성할 경우, 새로 생성한 UMat 객체가 완전히 소멸한 후 원본 Mat 객체 사용! (out of sync 방지)

> * 병렬 프로그래밍

![image](https://user-images.githubusercontent.com/55529455/160977992-5d8b9066-0829-417c-a24a-d6200bdb7f3b.png)
![image](https://user-images.githubusercontent.com/55529455/160978177-7dd98b97-8272-4bbb-850a-4a8f7172f029.png)
> * 각각의 그림을 잘라서, 계산하여, 합치는 방법을 이용하여 다양한 자원을 활용함.

![image](https://user-images.githubusercontent.com/55529455/160979011-a5a9f51a-e429-411f-9f4e-a6986290df7a.png)

> * 메모리 버퍼로부터 Mat 객체 생성하기
> * 사용자가 할당한 메모리 버퍼로부터 Mat 객체 생성하기
> * 외부 함수 또는 외부 라이브러리로부터 생성된 영상 데이터 메모리 버퍼가 있을 경우, 해당 메모리 버퍼를 참조하는 Mat 객체를 생성하여 사용 가능
> * Mat 객체 생성 후, OpenCV 라이브러리를 사용 할 수 있음.
> * 비디오 캡처를 위해서는 범용성을 보여야 한다. 범용성이 해결된다면, 그 때 퍼포먼스를 보아야 함. (카메라 제조회사의 레퍼런스를 따름, 코드 및 API 등)
> * memcopy를 이용하더라도 사진의 용량이 크면 시간이 걸림. 이 방법을 해결하기 위해 메모리 버퍼쪽을 가리키는 포인터를 통한 직접 조작을 수행.

![image](https://user-images.githubusercontent.com/55529455/160985214-2d69daa4-ca3f-401c-8c69-517928222fac.png)

> * 룩업 테이블 (LUT = Lookup Table)
> * 특정 연산에 대해 미리 결과 값을 계산하여 배열 등으로 저장해 놓은 것.
> * 픽셀 값을 변경하는 경우, 256 x 1 크기의 unsigned char 행렬에 픽셀 값 변환 수식 결과 값을 미리 저장한 함.
> * 이후 , 실제 모든 픽셀에 대해 실제 연산을 수행하는 대신 행렬(룩업 테이블) 값을 참조하여 결과 영상 픽셀 값을 설정

> * 코너의 특징
> * 평탄한 영역(flat), 에지(edge) 영역은 고유한 위치를 찾기 어려움
> * 코너(corner)는 변별력이 높은 편이며, 영상의 이동 및 회전 변환에 강력함.
> * 사각형을 기준으로 코너는 꼭짓점, 에지는 각 꼭짓점을 잇는 선, 플랫은 면을 의미함.
> * 특징 = feature = 영상을 표현 할 수 있는 어떤 속성. - ex) 히스토그램

![image](https://user-images.githubusercontent.com/55529455/160991950-029a4864-329c-4448-a96f-5b4308ecd38f.png)
![image](https://user-images.githubusercontent.com/55529455/160992907-b8936473-12a9-4aa6-852c-f0ef781a2a9b.png)
![image](https://user-images.githubusercontent.com/55529455/160992848-9b39fd56-cf7c-4da4-8bf4-abbcd1dba3d2.png)
![image](https://user-images.githubusercontent.com/55529455/160993360-8ee96ef5-7f52-4077-b2e9-71c5a865655a.png)

> *  FAST는 한 점으로부터 상하좌우 3개, 대각선 1개씩 해서 16개의 점을 처음 지정한 점과 비교하여 9개 이상의 점이 차이가 많이 나면, 코너라고 판단함.


