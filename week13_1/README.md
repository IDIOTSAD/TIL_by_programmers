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
* 

![image](https://user-images.githubusercontent.com/55529455/170920617-db371609-6fdc-4a57-b321-ce1ea89489c6.png)
