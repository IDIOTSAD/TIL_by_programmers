# 강의 요약

> chroot
> change root directory
> root dir.를 특정 디렉터리로 변경
> unix command 및 system call로 존재
> 초기 chroot의 사용 (SVr4)
> system 설치 및 복구 등 시스템 부팅 및 관련 과정에서 사용
> 부수적으로 jail의 기능을 가지고 있음 - FreeBSD의 경우, jail system call을 개발하기도 함.

> chroot의 부수적 기능
> 보안적 측면의 격리
> chroot를 통해서 기초적인 격리를 할 수 있다.
> sandbox의 개념 (격리된 공간의 타입)
> 격리된 형태의 공간을 필요할 때 사용함.
> 이는 개념적인 부분임 - 구현체가 아님
> 구현체 중에서 sandbox라는 이름이 실제로 있음. UNIX의 fifo named pipe (mkfifo) 파이프가 fifo의 개념과 이름만 같음을 상기
> chroot로 격리된 directory hierarchy를 통해 경로를 속일 수 있음.
> 즉, 동일한 프로그램을 쉽게 다른 환경으로 복제할 수도 있다는 사실을 알게 된다.

> 실습
> sudo apt -y install vsftpd
> sudo systemctl is-active vsftpd (active가 아니면, sudo systemctl start vsftpd)
> sudo apt -y install filezilla

![a](https://user-images.githubusercontent.com/55529455/163771682-68ca173e-47c1-4821-b4ec-510a40444a0b.png)
![image](https://user-images.githubusercontent.com/55529455/163772493-def0078e-ab6f-4e9d-a3ff-0ae46c457f16.png)
![image](https://user-images.githubusercontent.com/55529455/163772551-9a8c4079-5427-4a72-b195-7b60190f5ea1.png)

> Isolation
> 격리의 필요성
> 시스템 내에 존재하는 자원은 한정적 - 한정적인 자원을 효율적으로 분배하면 가용성 증가
> Process의 scope를 생각하자
> 현대적인 OS는 프로세스가 독립적인 공간을 가지게 해줌
> 장점 = 프로세스는 고유한 공간을 받을 수 있다
> 단점 = 외부 통신을 위해서 IPC를 사용하여 I/O비용이 높아짐
> 여러 프로세스가 협동해야하는 프로그램에서는 단점이 더 커진다 = DBMS, server system

> Isolation의 활용
> 1. 보안, 자원 관리적 측면
> 특정파일 경로의 접근 제한 = 특정 시스템 자원의 사용 제한 (chroot, 예를들어 FTP 프로세스가 /home/ftp 디렉터리 이하에서만 사용하고자)
> 호스팅 업체라면 고성능 컴퓨터 1대로 여러 사업자에게 DB나 웹 제공
> 2. 호환 충돌 측면 (바이너리 동시실행)
> 동일한 디렉터리를 사용하는 프로세스는 독립된 실행을 어떻게 할 수 있나?
> 혹은 서로 다른 버전의 파일을 사용하는 프로세스가 있다면?
> 예를 들면 서로 다른 version의 library파일을 사용해야만 하는 경우
> 프로세스를 동시 실행하는 것은 프로그램 수정을 통해 해결가능하지만, 내가 작성한 프로그램이 아니라면 소스코드는? 시스템에서 격리된 공간을 제공하면 문제 해결

> Name Space
> history
> The Use of Name Spaces in Plan 9 (1992) -> 분산 컴퓨팅 시스템으로서 local system, remote system을 hierarchical file system으로 표현 (path 표현)
> 특정 리소스의 사용은 계층화된 file name space를 가지는 것과 같음 - 이것은 directory service를 마치 chroot로
> Linux Name Space
> isolated resource를 NS의 hierarchical file system 형태로 구현
> 구현된 형태로 resource는 각자의 Dir를 가지게 됨.
> 줄여서NS라고도 함.

> Linux Name Space 종류
> mount, UTS(Unix Time-sharing), IPC, network, PID, user, cgroup
> binary - unshare, lsns, nsenter

> cgroup
> Process container - 2006 (Paul Menage, Rohit Seth
> Renaming : cgroup - 2007
> V2 : cgroup v2 - 2016 허태준
> OS level abstraction
> group별로 가상화된 공간을 만들고 자원을 제약 할 수 있게 됨.
> 다른 그룹은 격리되어있으므로 마치 물리적으로 다른 호스트처럼 인식
> docker, hadoop, systemd 수많은 프로젝트들이 cgroup을 사용

> LXC
> LinuX Container
> 현재 공식적으로 콘테이너를 지원하고 있으나
> 2008, IBM의 Daniel Lezcano와 Google의 협동으로 나옴
> 2014, v1.0 발표
> 특징 - 초창기 리눅스 컨테이너 기술의 발판 - docker의 경우도 초창기에는 lxc를 사용 (후에 교체)

> docker
> container runtime (2008 설립, 2013 릴리즈)
> Standard - docker(de facto), OCI v1.0 (2017) 제정
> OCI(Open Container Initiative)
> docker는 container를 세련된 방식으로 구현한 제품의 일종
> 격리된 자원의 묶음(image)와 런타임으로 구성
> 기본적으로 C/S 구조를 가지므로 daemon이 작동함.
> host OS위에서 작동되는 격리된 프로세스의 일종이므로 virtual machine과 달리 Memory, File system의 I/O에서 발생되는 크리티컬한 overhead가 없음.
> 위 부분이 docker의 큰 장점이 됨.
> 왜냐하면, HOST OS의 튜닝이나 성능 향상은 docker에게도 향상을 가져다 주기 때문이다
> 단점 = daemon 작동으로 인해 child process로 수직관리 - 관리자 권한 사용해야함.

![image](https://user-images.githubusercontent.com/55529455/163781356-b712d9fc-44ea-4850-b6cb-9b6c26c2f9f9.png)
> Podman
> alternative of linux container
> docker가 가장 많이 쓰이고 있지만, 단점과 상용화 문제로 인해 대안 요구
> podman은 Redhat에서 지원 - no daemon service, no admin account, systemd unit support (admin)

> Future of container
> docker
> 입지가 불안, 구조적 기술적 문제가 있지만 여전히 매력적인 기술
> docker의 대안이 계속되서 제안되고 있음
> 하지만, docker와 그 바탕이 되는 개념 (namespace, cgroup, virtualization, chroot)를 잘 이해하고 있다면 다른 container기술을 이해하는데 도움이 됨.
> container 기술의 복잡성 증가
> maturity level(숙성도) 높지않아서 자주 변경되는 개념

> Isolation : Virtual machine
> Full virtualization(Hpyervisor) 사용
> 소프트웨어로 가상화된 하드웨어를 구현 (실제는 없는 하드웨어 구성) - 완전한 격리된 공간
> 이를 통해 보안, 호환성 문제를 거의 해결 할 수 있음.
> 단점 : 낮은성능, 독점적인 자원 점유, Host-Guest 간 자원 교환의 어려움 및 비효율

![image](https://user-images.githubusercontent.com/55529455/163787423-8052d56d-84d9-4826-884d-6f302ee9b8ce.png)
> OS가 관리하는 H/W를 접근 방식 차이 = 직접접근, 간접접근 => VM을 사용하면 오버헤드가 커지는 단점이 있음.

> sandbox
> 사전적 의미 그대로 격리된 모래 장난을 위한 공간의 개념 채용
> 구현 - 다양한 방법이 가능 (VM, container, chroot)
> 목적 - 테스트 유닛으로서 격리된 공간, 보안공간, 복제된 서비스 공간
> 베타 버전프로그램 테스트 시, 다른 프로그램에 영향주기 싫을 때, OS를 매일 재설치는 비효율적이기 때문에 VM.

> sandbox의 격리된 공간의 장점
> 프로그램이 작동하기 위해서는 많은 외부 자원을 필요로 한다.
> 예를 들어 게임을 설치 시, directX, VC++ dist, ...
> 버전까지 맞춰야하는 경우도 있음. 버전이 다르면 충돌여부 검토
> 하지만 귀찮고 경우의 수가 많음.

![image](https://user-images.githubusercontent.com/55529455/163787763-08ae1f09-cbe5-4145-94c4-7fe3df8c3576.png)

> 요약
> chroot는 말 그대로 Root dir을 변경해줌.
> Isolation 할 수 있는 자원을 여러종류 있음.
> 이를 좀 더 편리하게 해주는 것이 container고, 기존에 나와있는 namespace, cgroup, chroot를 결합함.
> docker, podman등은 container의 구현체
> container의 가장 큰 장점은 성능과 배포
> VM, 특히, full virtualization은 성능 문제가 심각함.



















