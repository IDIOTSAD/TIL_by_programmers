# 1장 요약 (Package)
> * Linux Package system
> * RedHat = rpm, yum, dnf
> * Debian = dkpg, apt-get, aptitude, apt

> * 패키지
> * 시스템을 구성하는 파일의 묶음
> * 패키지 관리자 (설치 프로그램)에 의해서 읽혀지는 pre-built 파일들
> * 관리의 편리함을 제공함.
> * 리눅스 패키지 방식
> * RPM = 레드햇 계열
> * DEB = 데비안 계열

> * 데비안 계열의 주요 명령어
> * dpkg (debian package manager) - 기본 명령
> * apt (advanced package tools) - 네트워크, 의존성 설치 지원 툴
> * 레드헷 계열 주요 명령어
> * rpm (RedHat package manager) - 기본 명령
> * yum (yellow-dog updater modifier) - 네트워크, 의존성 설치 지원 툴
> * dnf

> * dpkg file 구조
> * debian package manager = unix의 pkg에서 유래됨.
> * extension - deb
> * package_name, version & release, arch(아키텍쳐)로 이름이 구성됨.

> * dpkg는 dependency를 제대로 해결하기 어렵고, 검색도 어려웠다. (네트워크 설치를 제대로 지원하지 못함.)
> * 이러한 문제로 인해서 APT가 등장하였고, 현재는 dpkg의 모든 기능을 배울 필요가 없다.

> * dpkg 파라메터
> * -l = list 출력
> * -s = 패키지 상태 확인
> * -S = 패키지 검색
> * audit = 패키지 문제 해결

# 2장 요약 (APT)
> * APT = debian의 dpkg를 랩핑한 front-end tool
> * 네트워크 설치 지원(미러 탐색 가능), dependency 탐색 및 설치 가능
> * binary(명령어) = apt-get(install, remove, update), apt-cache(쿼리)
> * binary-extensions = apt-file
> * 난잡한 문제로 인해서 (통일성이 없음) 해당 명령어로 통일됨. = apt

> * Source List
> * apt가 패키지를 가져오는 곳, 다운로드를 받는 곳의 정보, 로컬주소 or 네트워크 주소로 구성
> * etc/apt/source.list에 존재함.
> * 해당 위치에서 수정해도 되지만, /etc/apt/sources.list.d/에 \*.list 파일명으로 추가하는편이 좋음.
> * 편집시 apt edit-source 명령어로도 가능함.

> * source.list format
> * deb \[ optionl=valuel option2=value2 ] uri suite \[componet]
> * uri = 패키지를 제공하는 사이트의 uri
> * suite distribution codename 디렉터리 이름
> * componet = suite의 구성요소 및 라이선스 종류별 분류
> * 컴포넌트의 종류 = main, restricted, universe, security, updates 등
> * main = 공식 지원, restricted = 무료 라이선스, universe = 비공식 지원

> * /etc/apt/sources.list

![image](https://user-images.githubusercontent.com/55529455/158120370-fd408cb2-f8c4-4b4f-9321-132ac06254f2.png)
![image](https://user-images.githubusercontent.com/55529455/158120696-078bf96a-7b39-422f-90d9-b6985a56b8d3.png)
![image](https://user-images.githubusercontent.com/55529455/158120644-6c1d480e-cba0-449b-899f-277d309df18c.png)

> * 카카오 미러 설정하기
> * 편집할 파일 = /etc/apt/source.list.d/kakao.list
> * sudo select-editor를 이용하여 vim으로 설정
> * apt edit-sources kakao.list 명령을 친 후, 위의 사진에 나왔던 내용을 입력하고, 저장하여 나간다.

> * apt update = source list 갱신
> * apt search = 패키지 키워드를 검색 (-n 추가 시, 검색을 name 필드로 한정함)
> * apt show = 패키지 정보 출력
> * apt remove(패키지만 삭제), purge(패키지 config도 삭제), autoremove(의존성 깨지거나, 버전 관리로 인해 쓰지 않는 패키지 자동 제거)
> * apt install = 패키지 설치 (설치가 의존성 문제가 나면, universe를 추가하거나, 버전 다운그레이드)
> * apt list --all-versions 를 이용하여 버전을 확인한 후, 설치하면 좋음.
> * aptitude = apt-cache, apt-get 명령을 모두 포함한 apt 사용법.

# 3장 요약 (linux network system)
> * 국제 표준 문서 (Network에 설정에 필요한 기초 용어)
```
hotname = primary hostname, FQDN
TCP/IP = IP adress(v4, v6), subnet mask, gateway
NIC = Network Interface Card = 랜카드
Wired Network = 유선 네트워크
Wireless Network = 무선 네트워크
LAN = Local Area Network
WAN = Wide Area Network
```

> * 네투워크 이름 = hostname
> * 호스트 이름 = 사람의 이름에 해당하는 것. 떄에 따라 given name에 한정되는 의미를 말함
> * 도메인 주소 = 사람의 성에 해당하는 것.

> * FQDN, hostname
> * hostname은 중의적 표현이 존재함. (domain을 포함X, 포함하거나 - FQDN)
> * FQDN = Fully Qualifed Domain Name
> * fedora.redhat.com = hostname = FQDN = 도메인 내에서 유일하게 구별 가능한 이름
> * 도메인 주소는 체계적임. (kr 한국, or 단체, fclinux 단체의 이름, devel 단체내에서 유일한 컴퓨터 이름) ex)devel.fclinux.or.kr
> * 특별한 호스트 이름 = localhost = 항상 자기자신의 의미하는 주소, v4 = 127.0.0.1, v6 ::1

> * IPv4
> * version 4, 32bit 주소체계, 8bit씩 끊어서 읽음. XXX.XXX.XXX.XXX
> * IPv6
> * version 6, 128bit 주소체계, IPv4의 부족현상으로 만들어짐. Apple은 공식적으로 v6만 지원함.
> * IPv4-mapped IPv6 => ::ffff:IPv4_addr ex)XXX.XXX.XXX.XXX은 ::ffff:XXX.XXX.XXX.XXX.
> * link-local unicast = FE80::/10
> * Documentation IPv6 address prefix = 2001:D88::/32

> * dual stack
> * IPv6에는 TCP/IP 스택이 2개가 들어가 있음.
> * 지원되는 OS = 대부분의 OS, but XP 아래로는 지원 안함.

![image](https://user-images.githubusercontent.com/55529455/158122688-2203c046-4e0e-464a-8810-3e30e0e4b673.png)

> * 과도기에 자주 격는 문제
> * IPv4와 IPv6의 듀얼 스택의 문제 = 서버나 클라이언트가 IPv4에만 열려있거나..
> * 각각의 방화벽에 대한 문제 = 각 버전마다 다른 방화벽이 운용됨.

> * IP 클래스(A~E)가 없어지고, CIDR이 생김.
> * CIDR = IP 클래스와 상관없이 서브넷을 지정하여 자르는 것을 의미함.

![image](https://user-images.githubusercontent.com/55529455/158123189-24faf6f9-166b-4789-948e-0256f12f1f57.png)

> * public IP = 공인 주소 (인터넷에서 유일한 주소)
> * private IP = 사설 주소 (인터넷에 직접 연결 X)
> * NIC = 랜카드

> * SELinux와 네트워크 서비스
> * Security Enhanced Linux = 커널 레벨에서의 중앙 집중식 보안 기능 (우분투는 설치안됨.)
> * Security Enhanced Linux의 보안 레벨
```
enforcing (강제) = SELinux를 이용, 보안 설정에 걸리면 강제로 막음
permissive (허가) = SELinux를 이용, 보안설정에 걸리면 허용하되 로그 출력
disabled (비활성) = SELinux를 이용하지 않음.
```
> * 서버 구성시에는 SELinux에 대한 이해가 필요함. 강제는 어려우므로 허가레벨로 실습하면 좋음.

# 4장 요약 (Ubuntu Network config - legacy)
> * 네트워크 설정은 legacy, Networkmanager 방식이 있음.
> * legacy는 사용하지 않음. = 쓰지말라고 배우는 거임.
> * debian = /etc/network/interfaces
> * redhat = /etc/sysconfig/network-scripts/*
> * legacy 방식을 배우는 이유
> * 혹시나 legacy 방식을 사용하는 커스텀 리눅스를 사용하는 경우
> * 인터넷 검색을 잘못해서 legacy 방식으로 강제 설정한 경우

# 5장 요약 (NetworkManager)
> * NetworkManager의 장점

![image](https://user-images.githubusercontent.com/55529455/158127419-2840bb94-991e-4851-a39f-6f4b468e3757.png)

> * UNIX Standard command (POSIX)
> * ifconfig = interface config = query/control (구식)
> * route = routing table = query/control
> * Non-standard command (Linux specific)
> * ip = net, commands on EL6
> * nmcli = new commands on EL7 (networkmanager CLI)
> * ethtool, pifconfig & pethtool (python-ethtool)

> * nmcli
> * nmcli g\[eneral] => 현재상태 출력 => state(연결, 대기), connectivity(full/none)
> * nmcli n => 네트워크 상태 조회 (on/off)
> * nmcli dev => device 확인 (ens33에 주목)
> * eth# = old style 네트워크 디바이스 이름
> * Consistent network device naming (new style) = enp5s0, eno1 등등
```
en = ethernet
wl = wireless lan
ww = wireless wan
o = on-board-device
s = hotplug slot
x = MAC address
p<bus>s<slot> = PCI geographical location (device id 나옴)
p<bus>s<slot> = USB port number chain (port 나옴)
```
> * nmcli c\[onnection] s\[show] = 연결 상태 보여줌.
> * nmcli 주요 속성
> * IPv4 = auto | manual, auto = dhcp, manual = static ip
> * ipv4.addr = 주소
> * ipv4.gateway = 게이트웨이
> * ipv4.dns = dns 서버

> * nmcli con down (connections name) = 연결 끄기, nmcli con up (connections name) = 연결
> * nmcli con modify (new connection name) connection.id (device name) = connection 이름 변경
> * 고정 IP로 변경까지 한다면?

![image](https://user-images.githubusercontent.com/55529455/158129341-a2052cea-856e-47e4-addb-00cdde2c8118.png)

> * nmcli c del (device name) = 기존 설정 삭제
> * nmcli c add con-name (device name) ifname (device name) type ethernet ip4 (ip/서브넷마스크)
> * nmcli c mod (device name) +ipv4.dns (dns address) = DNS 추가
> * nmcli dev connect (device name) - 활성화
> * nmcli networking on - 활성화

# 6장 요약 (Network tools : ss ntstat)
