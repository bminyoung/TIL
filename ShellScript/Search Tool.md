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

























































