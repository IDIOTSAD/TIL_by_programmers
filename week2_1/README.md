# week 2_1

### ● 1강 요약 (리눅스의 역사, 배포판)
> * 유닉스, 리눅스의 역사를 배워야 하는 이유
> 1. 표준안(standard)의 존재 의미를 알려준다.
> 2. 지금도 표준화 이전의 세계가 존재한다.
> 3. 인터넷 검색에서 나오는 출처가 의심스러운 문서에 주의하자.
> * ### 따라서, 항상 표준 문서와 공식 문서를 먼저 보는 습관을 들이자.
> 4. 인과관계, 상관관계를 이해할 수 있게 된다.
> * 기술의 발전은 어떤 "결핍"을 해결하기 위해 만들어진다.

> * 표준 이전의 무질서한 세계
> * -> POSIX, X/Open, SUS : 현재 사용되는 표준
> * BSD, SysV : 과거 업계 표준

> * C언어와 UNIX/Linux 관계
> * -> ANSI C -> C99 : ISO/IEC 9899
> * -> C언어는 UNIX를 만들기 위해 탄생한 언어
> * UNIX, Linux의 호환이유는 표준덕분
> * Linux 배포판 : 레드헷, 데비안

> ### 키포인트
> * 다양한 표준을 기억하고, 메모한다. -> 표준을 이용하면, 호환성을 보장하는것
> * 컴퓨터 시스템에서 "개방적 호환성"은 "교환"의 효율을 높인다. -> 개방적인 표준이 주는 호환성의 장점 상기.
> * -> 표준을 근거로 만들어지는 SW, HW의 다양한 조합이 호환된다는 보장 -> 같은 규격으로 경쟁하니 가격과 품질 상승.
> * 공식 문서
> * UNIX : www.opengroup.org
> * Linux redhat : access.redhat.com
> * linux foundation : www.linuxfoundation.org

> * ### MAC 프로젝트 : Multics
> * GE, Bell lab(AT&T), MIT AI Lab의 MAC* 프로젝트의 산물
> * 운영체제의 복잡한 기능은 감추고, 시분할, 페이지/세그먼트 메모리 관리, 프로세스 관리, 파일시스템... 등등
> * 그러나 Multics 프로젝트는 망했고, Ken Topmson이라는 사람이 UNIX를 만들기 시작.
> * Ken Topmson은 UNIX를 게임용으로 만들었다. -> 직접 만든 게임을 빠르게 동작하기 위해서 UNIX를 설계.
> * DEC 운영체제를 밀고, UNIX를 설치 할 정도로 성공
> * 하지만, 어셈블리어로 작성하기 때문에, 새로운 제품이 나오면 재작성을 해야함.
> * 데니스 리치는 브라이언 커닝이 B언어를 개량하여 C언어를 개발하게 됨. -> 73년에 C언어로 된 UNIX 배포.

> * ### UNIX를 C언어로 작성하였을때의 장점
> * 하드웨어가 달라져도 rebuild, 수정으로 포팅이 가능함.
> * 그 결과 UNIX는 PDP-11, VAX 이후의 기계에도 보급.
> * 의도치 않게 C언어는 어셈블리어의 몰락을 가져오게 됨. -> 어떤 프로그램 언어가 발전하면 다른 하나는 도태됨.

> * ### C언어의 장점
> * 고급언어지만, 어셈블리어와 버금가는 성능 -> 어셈블리어로 변환하여 컴파일하기 때문
> * 낮은 추상화 지원 -> stdio, file 객체
> * 저수준의 하드웨어 조작 가능
> * 쉬운 언어적 특성 -> 지금은 쉬울까..?
> * C언어의 국제표준 = ISO/IEC 9899
> * ANSI-C(C89) = 89년도 표준, C99 = 99년도 표준 -> 현재 산업계의 실직적 표준, C11 = 11년도 표준

> * ### UNIX의 분열
> 1. AT&T UNIX -> 통신사는 서버/워크스테이션을 만들지 않음. 따라서 교환기, 빌링 OS로 이용.
> 2. 73년, SOSP -> UNIX, C 공식발표로 버클리 대학에서 관심을 보임.
> 3. BSD UNIX -> Ken Tompson이 75년 버클리의 객원교수로 가면서, UNIX V6 버전 배포, TCP/IP 네트워킹 도입, Bill Jon와 시너지. (Sun Microsystem 창업)
> * bill joy는 NFS, Solaris, TCP/IP, VI, Java 등을 개발함.
> * 라이센스 개념이 희박해서 분열됨. -> 70년대 후반 대학에서 UNIX를 사용했던 학생이 취직하면서 BSD가 퍼짐.
> * Ken Tompson이 구심점 역할을 하지 않음, 폐쇠적인 개발자들이 각자 필요한 기능을 추가하다보니, 호환성이 떨어짐.
![image](https://user-images.githubusercontent.com/55529455/154890594-b767ef77-5285-44e7-b9c2-a6c42a75ebd3.png)

### ● 2강 요약 (리눅스의 역사, 배포판)
> * ### 호환성 문제.
> * 프로그래밍을 위한 시스템 콜의 호환성 결여
> * 시스템 인터페이스를 위한 명령어나 디렉토리 구조의 호환성 결여
> * UNIX 벤더들이 클라이언트의 요구에 맞춰서 커스터마이징을 함.
> * -> 이러다보니, 각각의 UNIX 벤더마다 통신, 메뉴얼, 명령어가 틀리게 됨. 빌드와 실행 보장을 못함. 이로 인해 Java 탄생의 모티브가 됨.
> * 미 국무성에서의 강한 불만 표출 -> IEEE의 주도로 시스템 콜의 표준화 진행 -> POSIX 초안 발표 : POSIX.1 1003-1988 -> 규격을 안맞추면 미정부 조달 불가.

> * ### POSIX(파직스)는 UNIX 시스템의 최소한의 호환성을 요구함.
> * pronounce phazicks -> RMS(리차드 M, Stallman)이 작명 -> GNU를 이끄는 사람. 유명한 해커.
> * POSIX는 API의 문법과 작동에 대한 의미(세멘틱스)만 담고 있음. -> 느슨하게 작성됨.
> * POSIX 1003.1 = POSIX 1, POSIX 1003.2 = POSIX 2 -> 둘이 합쳐짐. IEEE std 1003.1 = POSIX 1
> * AT&T, SUN이 공조하여 산업계 표준을 만듬. = SVR4를 만듬. SUN은 SVR4를 이용하여 SunOS를 Solaris로 만듬.

> * ### OSF의 설립 (Open Software Foundation)
> * AT&T와 SUN의 반독점을 목적으로 설립된 비영리 단체
> * 마이너 벤더들이 자사의 UNIX가 사장될것을 우려하여 대항할 방법으로 사용. (HP, IBM, DEC)
> * OSF/1을 발표하게 됨. - 통합 유닉스 => 결국, BSD, OSF/1, SVR4 등 파편화가 심화됨.

> * ### X/OPEN
> * 84년 유럽의 컴퓨터 제조업체들이 OS의 표준화를 위해 출범된 단체
> * 표준화의 제정이 아닌 교육과 퍼트리는데 주력함 -> 표준화를 위한 가이드라인 제시
> * X/OPEN의 가이드라인 : XPG -> SVR4와 OSF/1은 XPG v3에 근거하여 제작됨.
> * 미국 유닉스의 메뉴얼인 man page 또한 여기서 기원되었음. -> SysV 계열의 벤더도 X/OPEN에 가입.
> * 우리가 사용하는 메뉴얼도 XPG의 산물, conforming to에 흔적이 남아 있음.

> * ### POSIX, SVR4, OSF의 관계
> * POSIX는 최소한의 호환성을 보장 = 공통 분모
> * UNIX는 혼잡한 상황이 되어버림. -> XPG의 목적은 표준을 퍼트리는것이기 때문에 말장난이 됨.
> * MS의 서버용 OS 제작으로 인해 망할 것이라는 전망. -> UNIX의 벤더들끼리 연합하게 됨.
> * OSF는 X/OPEN과 합병하게 됨. -> Open Group으로 변환.

> * ### SUS (Single Unix Specification)
> * SUSv1 = XPG 4.2, 혹은 UNIX95라 명명함. -> 1995 (issue 4.2)
> * SUSv2 = UNIX98 - 1998 UNIX 표준, (issue 5)
> * SUSv3 = SUS 2002 (issue 6)
> * SUSv4 = SUS 2007 (issue 7)
> * UNIX의 상표권 => AT&T - 노벨 - X/Open (OpenGroup)
> * Open System = UNIX로 간주.


### ● 3강 요약 (리눅스의 역사, 배포판)
> * ### UNIX 이후의 세계 - Linux kernel
> * 리눅스는 임시운영체제였음. -> GNU Hurd 커널의 개발이 지연이 됨.
> * PC에서 구동가능한 쓸만한 커널로 토발즈가 만든 Linux kernel을 지원하기 시작.
> * 그러나 80년대 인기였던 Micro kernel 방식이 아닌 Monolithic kernel방식으로 인해 타넨바움과 토발즈는 설전을 벌임.
> * 결과는 흐지부지, 시간이 흘러 Micro kernel 대세론은 꺽임.
> * 리눅스가 분열되지 않은 점은, 토발즈가 존재했기 때문이다. 자비로운 종신 독재자 BDFL
![image](https://user-images.githubusercontent.com/55529455/154896329-582fb914-a643-4ce9-90aa-c1a358f0e748.png)

> * ### GNU - Gun is not UNIX
> * 사실 Linux는 GNU의 컴파일러와 유틸리티 (GCC) 덕분에 개발이 된 OS.
> * 리차드 스톨맨이 리딩하고 있음.
> * 처음부터 Linux는 POSIX 표준안에 근거하여 작성됨. 비표준 GNU확장도 있는데, 표준안에 영향을 주기도 함.

> * ### FSF (Free Software Foundation)
> * 자유로운 개발과 배포를 막는 기존의 상업적 지적재산권 제도가 SW의 발전을 저해한다고 하여 설립됨.
> * GNU는 공개하였지만, GPL 공개라이선스를 요구함. - GNU를 통해서 UNIX 진영은 높은 생산성을 가질 수 있다.

> * ### BSD
> * BSD는 소송, 자금지원 끊김으로 인해 고사직전까지 가게 됨.
> * 4.3 BSD 개량 포기. 4.4 BSD Lite로 공개 - 자발적으로 BSD를 계승 = FreeBSD, NetBSD, OpenBSD의 등장

> * ### Mac OS
> * NextStep (BSD) MS에서 쫒겨난 빌게이츠가 개발하고, 애플로 들어가게 됨. -> 새로운 Mac OS X (Darwin)은 XNU기반 BSD 시스템.
> * 오픈시스템 특성인 포팅이 열려있음. (cpu 종속성 낮음, Arm으로도 이주도 같은 맥락)
> * SUS 이후의 BSD를 계승했던 OSX
> * SUS 표준을 대부분 만족하고 있다. - 따라서 Linux에서 구동되는 대부분의 소프트웨어는 쉽게 OSX에 포딩되었고, 개발팀에서도 OSX를 쉽게 받아들이게 된다.
> * 표준화 이후 UNIX는 생산성이 높기 때문에, Linux도 마찬가지. OSX를 사용하는 직원이 업무 생산성도 높다는 연구결과가 발표됨.

> * ### 리눅스의 성공요인
> * 소스코드를 오픈하고, UNIX 표준(POSIX, SUS)를 받아들여 빠르게 시장의 규모를 키웠다. 단기간에 상업용 수준까지 발전함.
> * 당시 폐쇄적인 IT업계의 분위기로 인해 운영체제와 컴파일러들은 매우 비싼 소프트웨어였고, 해당 소프트웨어로 개발된 프로그램도 비쌀 수 밖에 없었음.
> * 벤더들의 고압적인 태도로 인해 OS의 문제인지 판단하기 어려웠음. -> 따라서 오픈소스인 초기 UNIX를 원했고, Linux가 요구조건에 거의 부합됨.
> * 그 결과로 UNIX, Windows의 몰락을 가져왔다.

> * ### Linux Distributions
> * 배포판을 분류하는 기준 - 일반적으로 패키지 시스템으로 계열을 나눔.
> * DEB = Debian, Ubuntu, Mint
> * RPM = RHEL, CentOS, Fedora, SuSe
> * RH - CentOS의 경우, EPEL을 사용하는 경우가 많음.
> * Extra Packages for Enterprise Linux
> * Debian은 작고 가벼운 시스템 구축이 목적
> * Ubuntu = 예쁘고 사용이 편리한 데스크탑 리눅스 구축이 목적
> * Enterprise Server-side용 패키지 지원이 부족 = Debian 계열의 패키지 방식은 결함과 기능적으로 확장 불가한 구조임.
> * 인터페이스 = Xfce, compiz 등
> * 많이 쓰는 배포판 CentOS, Ubuntu, Fedora 등
> * CentOS = RHEL의 클론이라 엔터프라이즈 환경에서 쓰기 좋음 -> 포털 및 스사트업 기업이 가장 많이 사용
> * Ubuntu는 IOT에 많이 사용함. 그러나, 스파이웨어나 상용 소프트웨어를 포합 (Amazon)
> * Fedora는 최신기술을 확인하기 편리, 선행기술 개발, 보안 시스템 개발에 사용됨.
![image](https://user-images.githubusercontent.com/55529455/154900867-c0e329fe-25c8-49c8-9b38-0c0dbe427a02.png)
