# Search Tool
## 1. grep

```
# "George"로 시작, "Washington"으로 끝나는 부분 검색
$ grep "George.*Washington" president.txt

# -c : 단어 count
$ grep -c George president.txt
7

# -o : 해당 패턴이 매치하는 부분만 출력
$ grep -o 'George.*' president.txt

# -b : 파일 내 발견된 위치 정보 (바이트 옵셋)
$ grep -bo 'George.*' president.txt

# | : or
$ grep 'Donald\|Obama' president.txt
$ egrep 'Donald|Obama' president.txt

# POSIX 정규표현식
$ grep -E '^\d{1,2}\. George' president.txt
$ grep -E '^[[:digit]]{1,2}\. George' president.txt

# -i : 대소문자 무시 & -v : 지정한 패턴이 발견되지 않는 것을 찾을 때
$ grep -i 'richard' president.txt | grep -v 'Nixon'

# -A1 : 검색결과 뒷줄 출력(after) & -B1 : 검색결과 앞줄 출력(before)
$ grep -E '198[[:digit:]]\)$' president.txt
$ grep -A1 -B1 -E '198[[:digit:]]\)$' president.txt

# 첫 글자가 숫자가 아닌 것
$ egrep '^[^0-9]' president.txt

$ /sbin/ifconfig eth0 | grep 'inet addr' | cut -d: -f2 | awk '{print $1}'

# 일반 검색용 찾기 명령 (모두 일반문자로 해석)
$ fgrep '(1974' president.txt
```



## 2. sed

```
$ seq 1 100 > nums
$ sed -n '15,18p' nums
15
16
17
18

# George -> Tom 수정 (줄마다 한번)
$ sed 's/George/Tom/' president.txt | grep -n Tom

# g : 검색 결과 모두 치환
$ sed 's/1981/2981/g' president.txt | grep -n 2981

# -E : 확장된 정규표현식 지원
$ sed -E '/\(/s/\(.*//g' president.txt |more

# 마지막 글자 삭제
$ sed 's/.$//' president.txt

# 공백or탭문자가 2~5번 반복되면 이후 글자 삭제
$ SP=$' ';TAB=$'\t';sed -E 's/'"(${SP}|${TAB})"'{2,5}.+$//' president.txt

# 리눅스 포맷으로 변환 (캐리지 리턴 삭제)
$ echo -en msdos says "\"hello world\"\x0a\x0d" > msdos.txt
$ hexdump -C msdos.txt
$ sed 's/.$//' msdos.txt

# ([^:]*) : 콜론이 나올때까지의 문자열 -> \1 (치환)
$ sed -E 's/([^:]*).*/\1/g' /etc/passwd

# \u : 대문자로 변경
$ sed -E "s/\b(.)/\u\1/g" <<< "hello world"
Hello World

# \l : 소문자로 변경
$ sed -E "s/\b(.)/\l\1/g" <<< "HELLO WORLD"
hELLO wORLD
```



## 3. 중괄호 확장

```
# noname1 ~ noname9 파일 생성
$ touch noname{1,2,3,4,5,6,7,8,9}
$ ls
noname1 noname3 noname5 noname7 noname9
noname2 noname4 noname6 noname8

# dir1 ~ dir9 생성
$ mkdir dir{1..9}

# 계층화하여 폴더구조 생성
$ mkdir -p newproject/{lib,doc/{pdf,ppt,doc},src,include/sys,bin}

# eval : 입력 라인이 두 번 구문 분석됨 (코드를 동적으로 평가하는 데 사용)
# {1..$length} : 중괄호 안에서는 변수 확장이 일어나지 못함 -> eval 사용
$ length=40
$ eval printf -v line '%.0s-' {1..$length}

# "cp president.txt president.txt.bak" 과 같은 효과
$ cp president.txt{,.bak}
```



## 4. 명령 대체

> $(명령)

```
$ LANG=C; date
$ LANG=C; echo "today is $(date)"
$ LANG=C; echo "today is `date`"

# cd dir1 -실패 => mkdir~ 실행, DIR1에 pwd 저장
$ export DIR1="$( cd dir1 || { mkdir dir1 && cd dir1;}; pwd)"
$ echo $DIR1
```



## 5. 산술 확장

> $((산술식))

- 산술 확장 내부에서 변수명에 달러기호$ 생략 가능

```
$ v1=12
$ v2=$((v1+34))
$ echo $v2
46
$ v3=$(($v1+$v2)); echo $v3
58
$ v3=$((v1+v2)); echo $v3
58
$ ((v3++))
$ echo $v3
59

# C언어의 복합대입연산자
$ ((v3+=1)); echo $v3
60

$ if true; then echo true; fi
true

# true=0으로 취급, 숫자로서의 0은 거짓
$ if ((true)); then echo true; fi
$ if ((0)); then echo true; fi

# true=0 임을 확인 가능
$ if $((true)); then echo true; fi
0: command not found
```



## 6. exit와 종료상태

- exit : 쉘 종료
- exit 0 : 정상 종료 (0=true)
- exit 1 : 쉘 종료 시 오류 발생 의미

```
$ rm myfile;echo $?

$ rm myfile || { echo 'Could not delete file!'>&2; exit 1; }
```



## 7. 논리 연산

- cmd1 || cmd2 : cmd1이 성공적으로 실행되지 않으면 cmd2 실행

```
# dir 폴더가 없으면 dir 폴더를 생성
$ ls dir || { mkdir dir; }
```

- cmd1 && cmd2 : cmd1이 성공적으로 실행되면 cmd2 실행

```
$ cd mydir && ./myscript
$ make && make install
```













































