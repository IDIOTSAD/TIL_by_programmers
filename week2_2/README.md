# 1강 요약 (리눅스 필수 명령어)

> * 명령행 완성 기능 - <TAB>
> * i18n - i~n 사이의 알파벳 개수에 기인
> * LANG 환경 변수 설정은 = en_US로 설정하는게 좋음.
```
  메뉴얼 - man
  붉은색 - 매우중요
  초록색 - 중요
  보라색 - 구식 명령어
  취소선 - 쓰면 안되는 구식 명령어
```
```
리눅스 베이직 커멘드
파일 관련
path = pwd, cd, pushd/popd
file data / meta data
조회 = ls, file, stat, whitch, find
데이터 변경 = cp, mv, rm, mkdir/rmdir, readlink **
메타 변경 = chmod, chown
파일묶음 = tar, cpio
파일압축 = gzip, xz, zstd***
텍스트 에디터 = vim(vi)
텍스트 필터 = cat(tac), head, tail, less, sort
텍스트 리젝스 = grep (egrep), sed, awk
잡 컨트롤 = jobs, fg, bg
프로세스 컨트롤러 = kill, pkill, 트레이싱 = strace
네트워킹 = nc, curl, wget
디스크 = df
시스템 = free, top, ps, vmstat, pidstat, lshw
패키지 = yum, rpm, dpkg, apt
네트워크 스텟, 컨피그 = ss, nmcli, ssh, tcpdump, tshark
오픈 파일 = lsof
커널 = sysctl
디스크 = fdisk, parted, mkfs, fsck, mount, lsblk, blkid, grubby, udisksctl
보안 = ulimit, 유저 = useradd passadd
서비스 = systemctl
```
# 2강 요약
> * pwd = print working directory
> * cd = change directory - cd [경로] / 루트, ~ 홈, - 이전경로
> * 경로 생략시, 홈부터 시작함.
> * 절대 경로 = /로 시작하는 경로, 상대 경로 = .으로 시작하는 경로
> * ls = list file, -al, -ltr, -i 등등.
> * a = all, l = long, t = sort by mtime, r = reverse

> * 유닉스 file mode bit = 파일 권하는 나타내는 3+9bit 체계
> * 3bit는 SetUID, SetGID, Stickybit의 접근 권한을 가짐
> * 9bit은 파일의 owner, group, others의 접근 권한을 의미함
> * 표기방법 = Symbolic mode = "rwx" 심볼로 표현
> * Octal mode = bit를 8진수로 표기하는 방법
> * r = 4, w = 2, x = 1로 표기함. ex) 640 = rw-r-----
> * r - 읽어오기, w - 쓰기, x - 목록 링크 엑세스(접근만)
> * directory인 경우, readable file list, writable file, accessible
> * 파일 생성시 기본값 = 기본 mode는 umask 값을 뺀 나머지가 된다.
> * umask = 022면
> * 폴더는 777 - 022 = 755가 기본 mode
> * 파일은 666 - 022 = 644가 기본 mode

> * mkdir - make directory
> * rmdir - remove directory -> 이거 대신에 rm -rf 이용해서 다지움.
> * rc = recursively, force

> * cp - copy, mv - move, rename, rm - remove
> * cp, mv 복사할 파일, 복사위치

> * chmod 권한 파일이름 - change mode
> * chown, chgrp - 오너와 그룹을 바꿀 수 있음. root 유저만 가능

# 3강 요약
> * file = 파일의 타입 확인
> * magic 데이터 = /usr/share/file/magic
> * stat [option] <file> - option을 지정하면 디테일하게 확인
> * file의 meta data를 추출함. 파일이름, 생성, 권한, 변환 등 출력
> * 파일의 확장자가 바뀌어도 파일의 종류를 알 수 있음. magic 덕분.
> * cp한 데이터를 mv 하게 되면, Access, Modify는 그대로, Change는 바뀜
> * alt + . => 가장 마지막에 실행되었던 인수를 가져옴.

> * touch = 파일의 메타 정보 업데이트
> * 파일이 존재하지 않으면 빈 파일이 생성됨.
> * touch후, 다시 똑같은 파일을 touch를 하게되면 ACM이 업데이트 됨.

> * find - 중요한 명령어, find directory
> * n - 정확히 n인 경우 검색, +n n보다 큰 경우 검색(n포함), -n n보다 작은 경우 검색 (n포함)
> * -name filename 파일이름 검색
> * -size n 크기가 n인 파일 검색
> * -mtime n day 바뀐 날짜가 n인 파일 검색
> * -mmin n 바뀐 시간이 n인 파일 검색
> * -inum n inode number가 n인 파일을 검색
> * -samefile file file과 같은 inode를 가진 파일을 검색(= 같은 하드링크를 검색)
> * -maxdepth level = 탐색할 위치의 하위 디렉터리 최대 깊이가 level인 파일 검색
> * -mindepth level = 탐색할 위치의 하위 디렉터리 최소 깊이가 level인 파일 검색
> * ex) find . -name '*k.dat' -a -size 1M
> * => 현재 디렉토리에서 k.dat이고, 크기가 0-1메가바이트에 만족하는 파일 찾기
> * 검색 후 작업지시 = -exec 옵션 \; 또는 \+를 써야함.
> * \; - 매번 찾을때마다 명령어 한번씩, \+ 다 더한다음에 하나씩 실행.
> * ex) find . -name "*.tmp" -a -exec rm {} \;
> * "*.tmp" 파일을 지워라. {} 안에 "*.tmp"가 들어간다 생각하면 됨.
> * 여기서 디렉토리도 지우려면 rm -rf로 변환.
> * \+가 되어있으면, a.tmp b.tmp 한번에 명령어가 내려짐.
> * -\+ 단점 : 파일 수가 많으면 안됨. 실패뜸.
> * \;는 rm이 2천번 실행(프로그램 2천번 실행), \+는 1번 실행.
> * find 연습문제 1답 = find ./ -mtime -1 -a -type f > mtime_b24.txt
> * find 연습문제 2답 = find ./ -maxdepth 3 -mtime -1 -type f -a -exec cp {} ~/backup \;

# 4강 요약
> * stdio - standard input output
> * file channel - 파일에 입출력하기 위한 통로, 하드웨어에 직접X, 가상화 레이어의 일종
> * -> C언어의 I/O 인터페이스의 심플함을 가능하게 함
> * 파일 채널 - 파일에 입출력하기 위한 메타 정보를 가지는 객체 (프로세스 스코프 유효, 휘발성)
> * 파일 서술자 = 파일 기술자
> * -> 파일 채널들에게는 붙여진 유일한 식별자, 숫자로 명명, 0번부터 시작하여 증가.
> * 0 - stdin, 1 - stdout, 2 - stderr => 예약된 파일서술자

> * 파이프 - 프로세스 사이에 통신으로 사용됨
> * IPC (inter-Process Communication)의 일종
> * shell에서도 많이 사용하는 기능이다.
> * 파이프의 종류
> * 1. annonymous pipe (이름 없는 파이프, 임시) 2. named pipe (이름있는 파이프, 시스템에 남아있음.)
> * 프로세스들의 직렬연결 - small is beautiful의 철학을 가능하게하는 기능
> * 명령행에서 | 를 사용함. ex) A | B | C -> A의 출력이 B의 입력으로 됨.
> * wc - word count  (-l 사용하면 라인 수 카운트)
> * 1번 파이프 -> 임시로 생성되었다가 소멸되는 파이프 | 를 쓰면 생성됨. - 보통적인 파이프
> * 2번 파이프 -> FIFO Pipe, path+filename이 있기 때문에, mkfifo를 사용하여 생성

> * 방향 재지정
> * A > B => A의 stdout을 파일 B로 연결.
> * A < B => A의 stdin을 파일 B로 연결
> * A >> B => 방향은 >와 같고, 추가하는 모드로.

> * cat - stdout과 파일을 자유롭게 연결해주는 기본 필터
> * 파일 내용을 stdout으로 출력시, stdin 입력을 redirection해서 파일로 출력하는 용도로 사용.

> * 묶는 작업 - tar, cpio
> * -> 단순히 파일을 묶는 작업, 보관하는 목적이고, tar는 BSD, cpio는 SysV의 잔해
> * 압축 유틸 - gzip, bzip2, xz, zstd, lz4
> * -> 압축률은 xz > bzip2, zstd > gzip > lz4 순이다.
> * xz, zstd를 많이 사용하고, gzip은 옛날 사람이 사용함.

> * tar [ctxv] [f archive-file] files
> * c = 생성, t = 테스트, x = 풀어내기, v = 상세한 정보 출력
> * f archive-file = 입출력할 아카이브 파일명
> * --exclude file = 대상중에 해당 파일 제외

> * gzip [-cdflrv] <file>
> * -d = 압축해제, -c = stdout으로 결과 출력, -1, -9 = fast~better 압축레벨 지정
> * 압축 = tar c /etc/*.conf | gzip -c > etc.tar.gz
> * 해제 = gzip -cd etc.tar.gz | tar x

# 5장 요약
> * ln - make links
> * i-node = 실제 데이터와 연관된 링크
> * 하드 링크 - i-node를 찾아서 접근할 수 있게 해주는 링크 (경로명), 몇개의 하드링크가 있어도 전부 오리지널.
> * 심볼릭 링크 - 경로만 알 수 있는 링크, 직접 가봐야 같은 링크인지 알 수 있음
> * i-node = 파일의 메타 정보 및 관리용 객체, 파일은 1개의 고유 i-node가 있음.
> * i-node는 디스크 파티션에서 유일한 식별자.
> * 파일 메타 정보 - 시간 관련, 사이즈, 소유권, 권한

> * hard link 생성
> * same i-node를 가리키므로 동일 파티션에서만 생성가능.
> * regular file만 가능 -> directoryt나 devicefile등은 생성 불가
> * 실체를 가진 파일

> * symbolic link
> * 위치만 가리키므로 다른 파티션, 모든 종류의 file에서 만들 수 있음
> * 가리키는 대상의 UNIX 파일 모드를 따라가므로 권한은 777이고, 의미는 없다.
> * 절대 경로를 이용해서 만들어야한다.

> * which - PATH에 존재하는 파일을 검색함.

> * readlink - Symlink가 여러 단계로 가리키는 파일이 있을 수 있다.
> * 따라서 cannonical path를 따라가는 기능이 있다.
> * readlink -f <symlink>마지막 링크를 제외한 모든 링크가 존재할 때 성공.
> * readlink -e <symlink> 모든 링크가 존재할 때 성공.
> * A->B->C->D|-f|->E|-e|

> * canonicalization - 중요. 컴퓨팅 환경에서 실체를 가지는 standard, officaial의 의미를 가짐.
> * ex) 옆집 주소란 용어가 있다. -> 상대적인 주소
> * 철수의 옆집인지? 영희의 옆집인지 알 수 없음.
> * 따라서 철수로 한정하면, 옆집주소를 offical하게 해석할 수 있음. 이런 과정이 canonicalization 임.
> * 상대적인 의미를 해석한 후, stardard, official의 대상을 한정하는 행위.
> * symlink도 상대적인 거기 때문에 끝까지 가봐야 알 수 있음.

# 6장 요약
> * ps - 기본적으로 현재 세션의 프로세스들을 보여줌
> * pid = 프로세스 id, tty = 터미널 id, time = cpu 시간(점유), cmd = 프로세스 이름
> * ps -e (all process), ps -a (all processes both session leader 보여줌)
> * ps -f (full format) 밑의 내용이 추가됨.
> * uid = 프로세스의 소유권자 id, ppid = 부모 프로세스 id
> * C = cpu 현재 사용량, stime = 시작한 시간
> * ps -l (long format) 밑의 내용이 추가됨.
> * f = 프로세스 플래그, s = 상태 코드, pri = 실시간 우선순위, ni = 나이스 우선순위
> * sz = 사용되는 코어 이미지의 메모리크기, c = cpu 누적 사용량
> * ps -el => all, long
> * ps -ef => all, full
> * ps -ej => all, jobs (pid, pgid, sid, tty)
> * ps는 UNIX 표준화 후, 2가지 옵션을 지원하기 시작함.
> * ps axf = BSD 스타일 | ps -e --forest = SysV 스타일
> * 연습 = ps -ef | grep (파일) 요즘은 alias를 이용해서 bashrc에 넣어둠.

> * kill은 프로세스를 죽이는 명령어가 아님.
> * 실제로 프로세스에 시그널을 전송하는 기능임.
> * continue를 하거나 stop을 기능이 존재함. -> kill -l 명령으로 시그널 확인 가능
> * 시그널
> * sighup = hang up 연결이 끊겼을 때
> * sigint = interrupt 컨트롤C 누르면 발생함. -> 중지
> * sigquit = quit 컨트롤 \ 누르면 발생. -> 상태 메모리를 덤프하냐?
> * sigkill = kill 프로그램 죽임 -> 강제로 죽임.
> * sigsegv = segment violation -> 이상하게 죽어서 메모리에 침범하는것
> * sigterm = terminate -> 죽으라고 요청하는것.
> * sigttstp = temporary stop -> 컨트롤Z로 발생함. -> 일시정지
> * ex) kill 13011 -> sigterm 시그널 보냄
> * ex) kill -QUIT 13013 SIGQUIT 시그널 보냄
> * ex) kill -9 13012 9번 시그널(sigkill)를 보냄. (kill -KILL 13012 동일)

> * job control -> fore/back-ground process
> * fore-ground process = 현재 세션에서 제어 터미널을 가진 프로세스
> * back-ground process = 현재 세션에서 제어 터미널을 잃어버린 프로세스
> * Ctrl - Z = sigtstip 시그널을 포그라운드 프로세스에 전달
> * 작동 = 잠시 정지시킴 = 결과적으로 백그라운드에 정지 상태로 저장됨.

> * 세션 = 멀티유저 시스템에서 통신 객체를 구별하기 위한 것.
> * 세션은 제어 터미널을 가질 수 있다.
> * SID == PID 가 같은 프로세스를 세션 리더라고 부른다.
> * 세션 리더는 프로세스 그룹 리더를 겸한다.
> * 세션 리더로부터 파생된 자식 프로세스는 모두 같은 세션을 가진다.
> * 세션에 속한 제어 터미널을 소유할 수 있따는 의미 = 포그라운드 프로세스
> * 로그아웃시 세션이 파괴되면서 세션에 속한 프로세스들은 모두 종료
> * 참고로 파직스 C API의 setsid 함수로 new session을 열 수 있음.
  
> * 제어 터미널
> * 사용자의 제어를 받는 터미널 장치 (키보드)
> * CUI에서 멀티 태스킹을 위한 제어 방법
> * 제어 터미널을 소유한 프로세스는 키보드 입력을 가진다.
> * -> 포그라운드 프로세스
> * 하나의 세션에서 포그라운드 프로세스는 최대 몇 개까지 가능한가? -> 1개
  
> * 제어 터미너 규격
> * ps 명령어 출력에서 TTY 필드 부분을 보면 2가지 방식으로 출력됨.
> * pts/# = UNIX98 Psedo terminal system = SUSv2
> * tty# = console terminal
> * 세션에서 제어 터미널을 가지고 있지 않는 경우는 = ps의 TTY 필드에 ?로 나타남.
  
> * Process Group = PID = ProcessGroup leader
> * 프로세스 그룹 리더는 시그널 전파 기능을 가짐.
> * kill에서 음수의 PID 번호는 프로세스 그룹에 시그널을 전파하는 것이다.
  
> * daemon 프로세스 = Orphan process (session leader)
> * stdio를 모두 /dev/null로 리다이렉션을 걸고 - 비활성화
> * 컨트롤 터미널을 가지지 않은 프로세스
  
> * CTRL - C = SIGINT 시그널을 포그라운드 프로세스에 전달, fork된 자식 프로세스도 종료
> * CTRL - \ = SIGQUIT 시그널을 포그라운드 프로세스에 전달, 위와 같으나, core가 생성됨
> * jobs = stoped, 백그라운드의 리스트 출력
> * fg %# = jobs의 작업 번호 = %는 생략가능 - 지정한 프로세스를 포그라운드로
> * bg %# = 백그라운드 -> 러닝상태로
> * command & = 커맨드를 백그라운드에서 러닝상태로 실행함.

