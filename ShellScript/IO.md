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

