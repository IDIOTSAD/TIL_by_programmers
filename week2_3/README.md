# 1장 요약
> * vi - visual editor
> * UNIX / Linux에서 가장 많이 사용하는 에디터, 76년 BSD Bill Joy가 개발 

> * vim - vi improved
> * vi에 추가적인 확장 기능 부여
> * 리눅스에서는 vim이 사용됨. - root가 사용하는 vim은 최소화된 vim
> * -> static linking 된 바이너리임.
> * 대부분의 UNIX에서도 complementary package로 제공됨.
> * 다양한 플랫폼을 지원함.
```
vim [filename]
ex) vim text.txt
ex) find . -name "*.txt" | vim - (파일명이 - 인 경우 stdin을 의미함)
vi의 기본 작동모드 - 일반, 입력, 명령행 (vim은 비주얼모드 추가)
비주얼 모드는 드래그 추가
일반 => 입력 가려면, a, i, o, A, I, O, R
입력 => 일반 가려면 esc
일반 => 명령 가려면 :
명령 => 일반 가려면 esc
a, A = append, 커서 위치에서 한칸 이동한 후, 입력모드 전환
i, I = insert, 현재 커서위치에서 입력모드 전환
o, O = open line, 현재 행 아래에 새로운 행 하나 만들어서 입력모드 전환
R = replace, 모든 글자는 덧쓰여짐.
force 명령 = !를 뒤에 더하여 이용함.
일반 모드가 필요한 이유 = GUI가 없기 때문에 short-cut으로 구현함.
```
> * vi의 커서 이동
```
h - 왼쪽, j - 아래, k - 위,  l - 오른쪽
^(caret, 캐럿) - 행의 맨 앞으로, $ - 행의 맨 뒤로
ctrl + b = page up = 위로 한 화면 스크롤
ctrl + f = page down = 아래로 한 화면 스크롤
ctrl + u = 위로 절반 스크롤
ctrl + d = 아래로 절반 스크롤
```
> * 라인이동
```
[#]gg = #행으로 이동, #이 생략되면 1
[#]G = #행으로 이동, #이 생략되면 마지막
:# = #행으로 이동
ctrl + g = :file = 현재 문서 위치 정보를 상태바에 표시
```

# 2장 요약
> * vi 삭제
```
x = 커서에 위치한 문자 삭제
dd = :d 현재 행을 삭제 (3dd 하면 3줄이 짤림)
D = 현재 컬럼 위치에서 현재 행의 끝부분까지 삭제(d$와 동일)
J = 아래 행을 현재 행의 끝에 붙임(아래 행의 앞부분 공백 제거)
```
> * 복사, 붙여넣기
```
p = 현재 행에 붙여넣습니다 (5p 하면 5번 행 붙이게됨.)
:pu 개행 문자가 포함된 경우에는 현재 행의 아래에 붙여 넣음
P = 행의 위쪽에 붙음.
yy = :y = Y 현재 행을 레지스터에 복사함.
u = undo 기능, 이전에 행한 명령 1개 취소
ctrl + r = redo 기낭, 이전에 취소했던 명령 다시 실행
```
> * 명령행 모드에서 범위를 지정해서 명령
```
:20d = 20번 행 삭제
:10, 25d = 10 ~ 25행 삭제
:10, $d = 10 ~ 마지막행 삭제
:%y = 문서 전체를 복사 (% =1,$)
:., +20y = 현재행부터 아래로 20행 복사
:-10, +5d = 위로부터 10행~아래로 5행 삭제
:40pu = 40번 행에 레지스터 내용 붙여넣기
. 현재 행
$ 마지막 행
+# 현재 위치에서 #만큼 아래 행
-# 현재 위치에서 #만큼 위 행
$ 문서전체
```
> * 비주얼 모드
> * 마우스의 드래그 기능을 대신함.
```
v = 현재 커서위치에서 블록 지정
V = 현재 커서가 위치한 행에서 행 단위로 블록 지정
ctrl + V = 열 단위로 블록을 지정함. (윈도 환경에선 ctrl Q도 가능)
비주얼 모드에서 : 를 누르면 자동으로 범위가 설정됨.
비주얼모드 - column editing
esc 2번 타이핑 해야 column editing이 완료됨
i = insert , a = append , c = change, ~ = switch case
특정 열에 문자열을 삽입, 교체하는 경우
gv = previous highlighted text 영역 불러오기
o = highlighted text 블록의 시작, 끝 이동 (블록의 위 아래를 재조정할때)
```
# 3장 요약

# 4장 요약
> * help
> * vim은 online hep를 지원함. = help (접두어) (문자)
> * 일반 = 없음, 입력 = i_, 명령행 = :, 비주얼 = v_
> * vim 실행인수 = -, 옵션 = ', 명령행 모드 특수키 = c_
> * help 볼때, 녹색 글씨에 모르는게 있으면 = ctrl + ], 되돌아오기 ctrl + T
> * help를 끌땐 :q, 왔다갔다 하고싶으면 ctrl w w

> * 자주 등장하는 오류
> * 1. 파일을 중복해서 오픈한 경우.
> * 읽기 전용 혹은 나가기 -> O 또는 Q를 추천.
> * 2. vim crash로 swapfile이 제거되지 못한 경우
> * R을 눌러 리커버리 한 후, 저장 후 종료하거나 delete 하는 방식을 이용한다.
> * 아니면, 스왑을 바로 삭제하는 방법으로 d키를 누르면 삭제됨.

# 5장 요약
> * formatting - center, right, left
> * width 기준으로 정렬을 함.

> * find - 문자 1개를 검색
> * fc = 문자 c를 전방검색, Fc = 문자 c를 후방 검색 ; = 최근 검색을 재검색,  ,= 최근 검색을 반대방향으로 검색
> * /string = string을 전방탐색함. /M, /V로 magin 탐색을 끌 수 있음. (magic = 특수문자에 대한 해석하는 기능)
> * ?string = string을 후방탐색함.
> * * 현재 커서에 위치한 단어를 전방탐색함.
> * # 현재 커서에 위치한 단어를 후방탐색함
> * n 다음 탐색 결과를 찾아냄
> * N n과 반대방향으로 다음 탐색
> * % 괄호의 짝을 찾아줌
> * [a-g]re = 정규표현식으로 검색하기.
> * /\c 하게 되면, 대문자 소문자 구분 없음.
> * :nohl 일회성 highlightsearch 해제
> * :set nohls highlightsearch 옵션 해제 (기본값으로 off된 경우도 있음)

> * substitute
> * 교체 = sed의 기능이 import 된 것.
> * 그래서 sed의 문법과 동일하다. (sed를 알면, 이 부분은 공짜 점심)
> * :[range]s/찾는 문자열/교체할 문제열/옵션 (예시 : :%s/ctrl+V+M//g)
> * separator로 slash가 주로 사용되지만, 다른 문자를 사용해도 무방하다 (콤마)
> * g = (global) 검색된 문자열 모두를 교체 (g 없으면 1개만 교체)
> * i = 대소문자 무시
> * c = 교체할 때마다 yes/no 물어봄
> * e = 교체 과정 중 에러 무시
> * 만약에 교체할 문자자 /가 있으면? ,를 이용한다. 아니면 이스케이프 \를 사용한다.

> * 특수문자의 교체
```
DOS/WINDOWS = CR + LF
UNIX = LF
UNIX => DOS 하려면 CR의 입력을 해주어야함. = Ctrl + V + M
하지만 NewLine 문자를 바꾸기 위해 위 방법은 안씀.
:set ff=dos 혹은 :set ff=unix로 설정 후 저장하는 방법을 쓴다.
아스키를 코드값으로 입력하는 경우
<CTRL-V> ### = ###에 10진수를 사용하여 아스키입력
<CTRL-V> o## = 8진수
<CTRL-V> x## = 16진수
숫자 증감 = 숫자 위에서 Ctrl A, Ctrl X를 누르면, 숫자를 즉시 증감할 수 있음.
A = 1증가, X는 1감소 (16진수 8진수도 됨.)
```

# 6장 요약
> * vim terminology
> * buffer = 파일을 편집하기 위한 임시공간. = 파일명없이 vim 실행시 버퍼에 저장하고있음.
> * register = 텍스트 일부를 저장하고 있는 임시 공간

> * edit, find
> * :e [filename] 파일을 편집모드로 오픈한다. 생략되면 현재 파일을 다시 엶.
> * :e #[count] 카운트번째 파일을 오픈한다. 카운트가 생략되면 이전 파일이다.
> * :find filename 파일이름에 해당하는 파일을 검색하여 오픈한다. 복수면 오류출력
> * CTRL ^ 명령어 단축키로서 ":e #"과 동일함 = CTRL + 6을 의미함.

> * 다중 파일 사용
> * vim 파일1 파일2 파일3 = :n으로 오른쪽이동, :N으로 왼쪽 이동.

> * quit
> * :q[!] 현재창 종료. !는 강제 종료(저장안할때 유용)
> * :qa[!] 모든창 종료
> * :wq 저장하면서 종료
> * :wqa 저장하면서 모든창 종료

> * write, update
> * :w [filename] 파일이름이 지정되면 해당 파일에 쓰기를 지정
> * 생력되면 현재파일에 쓰기 지정, 사본을 만든 경우는 편집중인 파일은 원래 파일로.
> * :sav file 현재파일을 다른 이름으로 저장함. 편집중인 파일도 새로 저장된 파일로 교체
> * :up 변경된 점이 있는 경우 ":w" 실행
> * :x up+quit, 일반모드에서는 ZZ(shift z) 사용.
> * 예시)10, 50w history 10~50행 history에 저장

> * netrw = vim으로 디렉터리 열기 (브라우징 기능)
> * 실행 방법 = 현재 디렉토리를 vi에서 :e .를 이용하여 열고, 파일 열고 나갈때는 Ctrl + 6을 눌러서 나감
> * enter = 파일 열기
> * i = 파일 표시방법 변경 (한줄, 파일 정보, 와이드, 트리)
> * s = 정렬 방식 변경 (이름, 시간, 크기)
> * o = 수평 분할
> * v = 수직 분할
> * p = 커서위치 파일을 미리보기로 열어줌
> * t = 새로운 탭으로 분할해서 열어줌.
> * - = 상위 디렉터리로 이동.
> * 예시) ctrl + w v/ :vs [file]

> * 창분할, 생성명령 - #은 창의 크기
> * :[#]sp [파일명] 상하로 창 분할, 파일명 생략시 현재파일
> * :[#]vs [파일명] 좌우로 창을 분할
> * :[#]new = 상하로 분할, 새로운 창 만듬.
> * :[#]vnew = 좌우 창분리 후, 새로운 창 만듬.

> * 창 이동
> * Ctrl + w + 방향키 = 방향키로 이동 (h,j,k,l)
> * Ctrl + w + w = 현재창에서 오른쪽 방향으로 이동.
> * Ctrl + w + p = 이전에 사용한 창으로 이동
> * Ctrl + w = 동일하게 창분할
> * Ctrl + w [#]+ #크기만큼 크기 키움 (# 생략시 1)
> * Ctrl + w [#]- #크기만큼 크기 줄임

> * diff =  - vimd -d file1 file2 (diff 기능은 매우 중요함. 소스코드 비교할때, 설정파일 비교할 때 많이 쓰임)
> * do, dp를 사용하여 get, put 가능

> * 분할 창의 단점 = 분할 할때마다 원래 창의 크기가 줄어든다. => 탭 페이지 기능이 필요함.
> * 탭 열기 vim 실행 옵션 = -p (vim -p file1 file2)
> * :[#]tabe[dit] file #번쨰 탭에 파일을 연다. # 생략 시 다음 탭에 생성됨, 번호는 0번부터 시작.
> * :[#]tabnew file #번째 위치에 비어있는 탭을 만듭니다.
> * :[#]tabc[lose] #번째 탭을 닫습니다. 생략시 현재탭을 닫음.

> * 탭 사이 이동 명령 = key map이 편하다.
> * :[#]tabn[ext] = 다음 탭으로 이동하며, 일반 모드의 gt와 동일, #에 숫자를 지정하면 탭 번호가 생성됨.
> * [#]gt, [#]<CTRL - PageDown>
> * :[#]tabp[revious] = 이전 탭으로 이동하며 일반모드의 gT와 동일함.
> * [#]gT, [#]<CTRL - PageUp>
> * :tabm[ove] [#] #번째 탭으로 현재 탭을 이동시킴. (0부터 시작) #이 생략되면 가장 오른쪽으로 이동

> * vim buffers = file
> * 왜 버퍼라고 하는가? 저장 이전이면 이름이 없는 공간에 저장되어 있기 때문.
> * % 현재 버퍼, # 이전 버퍼, a 활성화된 버퍼, + 변경된 부분이 있는 버퍼
> * 커서 아래의 파일명을 인식하여 오픈하는 기능
> * -> gf(이동), Ctrl ^ (이전 파일로 되돌아가기) = 이 기능은 프로그래머에게 유용함.
> * -> Ctrl w f =커서 위치의 파일명을 분할된 창에 열어줌. Ctrl w gf =커서 위치의 파일명을 탭에 열어줌. 

# 7장 요약
> * fencs = 파일을 읽을 떄 확인할 encoding list를 설정
> * - 설정된 리스트를 순서대로 확인하면서 변환이 필요한 경우를 지원함. - .vimrc에 설정해야만 multi-bytes 기반 인코딩 파일을 읽기가능.
> * set fencs=value 예시) fence=ucs-bom,utf-8,korea,latin-1
> * bom 확인 후, 순서대로 확인하고, 마지막엔 아스키를 체크.
> * BOM (Byte Order Mask)
> * UCS(Universal coded Character Set)의 판별 마크 = 주로 생략하나, 관습적으로 옵션 설정시 앞부분에 넣음.

> * fenc, fencs에 사용가능한 문자세트 (encoding-values 도움말 참조, :help enco~~)
> * utf-8,utf8 = utf-8 유니코드 형식
> * ucs-bom BOM 마크에 의한 유니코드 형식
> * korea 한글 지원(별칭), 유닉스에서는 euc-kr, 윈도에서는 cp949로 자동 변환
> * japan 일본어 지원(별칭), 유닉스에서는 euc-jp, 윈도에서는 cp932로 자동변환
> * latin1, ansi 영문 ASCII 형식
> * 변환 방법
> * :set ff=unix => :set fenc=utf8 => :wq (다른 이름으로? :sav 파일이름)

> * 단어 경계이동
> * w키를 누를때마다 단어의 앞에서 커서가 멈춤.
> * e는 단어의 뒷부분에서 커서가 멈춤.

> * 단어경계이동 단축키
> * 0 0번째 열
> * ^ 공백이 아닌 실제 내용이 있는 시작 열
> * $ 마지막열(행의 끝)
> * w 단어의 시작 위치 혹은 문장부호의 경계를 따라서 이동
> * e w와 같으나, 단어의 끝 부분에 위치
> * b w와 비슷하나, 진행방향이 역방향임.
> * W, E, B 소문자와 기능이 비슷하지만, 단어가 가진 의미를 따져서 이동함.

> * 괄호, 문단, 블록 단위 이동 단축키
> * % 가장 가까운 괄호 짝으로 이동 - 중요
> * (, ) 문장 단위의 시작, 끝 위치로 이동
> * {, } 문단 단위의 시작, 끝 위치로 이동
> * [[, ]] 블록 단위의 시작, 끝 위치로 이동

> * abbreviation = 특정 단어 입력시 대체 입력하는 기능
> * ab, ia 기능을 이용
> * ia = insert mode에서만 작동하는 기능
> * ca는 commandline mode에서만 작동하는 기능
> * 예시) ab 내멜 sunyzero@gmail.com
> * 예시) ia 시간0 <C-R>=strftime("%Y. %m. %d - %H:%M%S")<CR>
> * ca 기능을 이용하면 오타를 변환할 수 있음. .vimrc 파일이 EUC-KR로 되어있으면 UTF-8문서 편집시 작동하지 않을 수 있음.
> * 예시) ca ㅈ w

> * key map
> * nmap 단축키 명령 - normal mode에서만 동작
> * imap 단축키 명령 - insert mode에서만 동작
> * map 단축키 명령 예시) nmap <F2> :up<CR>, imap <F4> sunyzero@gmail.com
> * n = 일반, i = 삽입, v = 비쥬얼, c = 명령행 <#>map

> * autocmd = 특정 상황에서 자동으로 실행할 명령
> * 예를 들어 *.c 파일을 열때 자동으로 실행되어야 하는 명령
> * autocmd BufRead, BufNewFile *.txt colo evening
> * autocmd BufRead, BufNewFile *.java colo morning|setlocal ts=2 sw=2
> * au SwapExists * let v:swapchoice = 'o' 
> * v:swapchoice = 'o'  -> 스왑파일이 존재한느 경우 o = readonly
> * v:swapchoice = 에서 e 또는 q 삽입 가능
> * 특정 경로명 패턴을 인식 시킬 수도 있음.
> * autocmd BufRead, BufNewFile */include/* colo slate|setlocal ts=8 sw=8

> * re-indenting (다시 들여쓰기)
> * ={motion} motion에는 이동 관련 키 gg, G, )), ]] 등을 사용할 수 있음.
> * visualmode + = 비주얼모드로 라인 선택 후 = 키를 눌러도 된다.

> * tab vs whiltespace
> * 기존에 작성된 탭 문자를 공백 4칸으로 전환하고 싶으면?
> * :set et ts = 4
> * :ret (ret 대신에 re-indenting 기능을 사용하는 편이 좋다.)
> * 반대로 공백 4칸을 탭 문자로 전환하고 싶으면?
> * :set noet ts = 4
> * :ret!

> * 자동완성기능
> * vim은 #include 구문도 이해함.
> * Ctrl + N 단어오나성을 위해서 현재 문서와 관련 파일을 전방탐색
> * Ctrl + P 위의 명령어의 반대로 탐색
> * 만약 특수문자가 섞인 내용을 탐색하려면? sunyzero@gmail.com
> * suny<Ctrl + N><Ctrl + X><Ctrl + N>....
> * <Ctrl + N><Ctrl + X> = 더하기 낲말 모드로 작동하여 추가 검색을 함. 원하는 낱말이 아니면 Ctrl + N을 계속 누르면 진행
> * <Ctrl + X><Ctrl + K><Ctrl + N> 사전 검색모드로 작동함.

> * vim-bootstrap = 자동으로 vimrc를 만들어 주는 곳.
> * https://vim-bootstrap.com
> * 여기서 만들어진 vimrc를 약간 수정하여 사용하는 사람이 많음.
