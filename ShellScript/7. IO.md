# IO
## 1. 입출력

- Bash 스크립트 입력의 방법
  - 명령 줄 인수
  - 환경 변수
  - 파일
  - 파일 기술자(file descriptor)로 표현 가능한 파이프, 터미널, 소켓 등
- Bash 스크립트 출력의 방법
  - 파일
  - 파일 디스크립터로 표현 가능한 다른 것
  - 다른 프로그램에 명령 줄 인수로 전달
  - 다른 프로그램에 환경 변수의 형태로 전달



## 2. 위치 매개 변수

```
# png 파일의 확장자를 JPG로 변경
$ ../rename.sh png JPG

#### rename.sh 파일
#!/bin/bash
fo name in *.$1
do
	mv $name ${name%$1}$2
done
```

- 매개변수가 10개 넘어갈 경우 중괄호를 써주어야 함 (ex. ${10})



## 3. 환경변수 & export

```
$ echo LANG
en_US.UTF-8

$ LANG=ko_KR.UTF-8 date
(date에만 locale 적용)

$ LANG=ko_KR.UTF-8

###
로그아웃 후 로그인 하면 locale 초기화
###

$ LANG=ko_KR.UTF-8
$ bash
# 스크립트에서도 유효

$ echo $LANG; ( echo $LANG in subshell; ); echo $LANG
# 서브쉘에서도 유효


## 일반 변수일 경우 - 스크립트에서는 유효하지 않음, 서브쉘에서는 유효
$ LANG1=ko_KR.UTF-8

# 일반 변수 사용
$ export LANG=ko_KR.UTF-8
```

- export 된 변수는 환경변수



## 4. 변수의 범위

```
$ year=2020

# 함수 내부에서도 유효
$ function sub(){ echo year=${year} in function; };sub
year=2020 in function

# 함수 내부에서 재할당한 값도 유효
$ function sub(){ echo year=${year} in function; year=4050;};sub; echo year=${year} in outer
year=2020 in function
year=4050 in outer
```

- 쉘 변수는 기본적으로 **전역변수**

```
# 바깥에서 선언된 변수는 스크립트 안에서는 유효하지 않음
$ echo 'echo year=$year' > mydate.sh
$ chmod +x mydate.sh
$ ./mydate.sh; echo year=$year in outer
year=
year=4050 in outer

# 스크립트 안에서의 변수 변경도 유효하지 않음
$ vim mydate.sh
echo year=$year
year = 9999
$ ./mydate.sh; echo year=$year in outer
year=
year=4050 in outer
```

- 쉘 스크립트는 변수에 관해 sandbox로 이해

```
$ year=2020;( echo year=${year} in inline; year=4050; ); echo year=${year} in outer
year=2020 in inline
year=2020 in outer
```

- 서브쉘 바깥에서 선언된 변수가 서브쉘 내에서 접근이 됨 (복제)
- 서브쉘 바깥의 변수에는 영향x

```
$ year=2020;{ echo year=${year} in inline; year=4050; }; echo year=${year} in outer
year=2020 in inline
year=4050 in outer
```

- 인라인그룹은 명령어를 묶어놓은 것 -> 바깥의 변수에도 영향

```
$ export year=2020;./mydate.sh; echo year=$year in outer
year=2020
year=2020 in outer
```

- 환경변수는 스크립트 내에서 변경해도 유효하지 않음



## 5. 파일 디스크립터

>FD(File Descriptor)
>
>프로그램이 파일을 참조하는 방식
>
>또는
>
>파일(파이프, 장치, 소켓 또는 터미널)처럼 작동하는 다른 리소스를 참조하는 방법

- 데이터 소스에 대한 포인터와 비슷
- 기록 가능한 장소와 같은 것
- FD의 리소스에서 데이터를 읽거나 씀

- 모든 프로세스는 3가지 열린 디스크립터를 가지고 있음
  - 표준 입력(stdin) : fd 0
  - 표준 출력(stdout) : fd 1
  - 표준 오류(stderr) : fd 2

```
# 표준 출력장치 사용 (fd 1)
$ echo hello world
hello world

# 표준 오류장치 사용 (fd 2)
$ ls dir33333

# 표준 입력장치 사용 (fd 0)
$ read -p "key press"
```



## 6. 리다이렉션

> 출력 내용을 파일로 저장 or 파일 내용을 다른 파일로 옮기기

```
$ echo "The seagull" > seagull.txt
$ cat seagull.txt
The seagull

#위와 같음
$ echo "The seagull" 1> seagull.txt

# > : 기존 파일에 덮어쓰기 (없으면 생성)
$ ls dir333 2> err.log

# >> : 기존 파일에 추가
$ ls dir444 2>> err.log

# 파일 합치기
$ echo ABCD > file1
$ echo 1234 > file2
$ cat file1 file2 > file
$ cat file
ABCD
1234

# < : 파일을 읽어서 while의 변수로 넣음
$ while read v; do echo $v; done<file
ABCD
1234

# 표준출력 -> 파일로 저장 (>)
# 표준에러 -> 파일로 저장 (2>&1)
$ echo "Jurassic World" > steven.txt 2>&1
$ grep "Star Wars" steven.txt lucas.txt 2>&1
grep: lucas.txt: No such file or directory
```







