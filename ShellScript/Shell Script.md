# Shell Script

## 1. Shell Script
> 명령 인터프리터 (Command interpreter)

- 사용자가 OS에 **대화식**으로 명령을 내리거나 **일괄**적으로 실행할 수 있는 기능을 제공하는 응용 프로그램
- 사용자가 시스템과 대화할 수 있는 방법

- 커널: OS의 코어부분, 하드웨어를 운영
  - 사용자나 응용 프로그램에 시스템 제반 기능을 서비스 형태로 지원

- 쉘: OS의 중심부
  - 사용자와 상호작용
  - 요구사항을 커널로 전달



## 2. 작성 방법

- 파일 맨 앞에 `#!/bin/bash` 입력: 쉬뱅(해시뱅)
  - /bin/bash 가 주된 실행자

```
<hello world.sh 파일>
#!/bin/bash
echo hello world
```



- /bin/bash가 없어도 (bin에 bash가 없어도) 실행 가능

```
<hello world.sh 파일>
#!/usr/bin/env bash
echo hello world
```



## 3. DOS스타일의 줄끝

- LF: Line Feed
- CR: Carriage Return
- linux: LF
- windows: CRLF
- 쉘에서 동작하는, 리눅스에서 사용하는 파일은 windows의 편집기는 피할 것



## 4. 실행 방법

```
# 실행 권한 주기
$ chmod +x helloworld.sh

# 1. 경로
$ ./helloworld.sh
hello world

# 2. bash
$ bash helloworld.sh
hello world

# 3. source
$ source helloworld.sh
hello world

# 4. dot
$ . helloworld.sh
hello world
```



## 5. 특수문자

#### 1) 공백 (white space)

- 탭, 줄 바꿈, 세로 탭, 양식 공급, 캐리지 리턴 또는 공백
- bash는 공백을 사용하여 단어의 시작, 끝을 결정
- 명령어 입력 시 첫번째 단어는 **명령 이름**, 추가 단어는 해당 명령에 대한 **인수**



#### 2) 확장 (expansion)

> $

- 다양한 유형의 확장을 도입

1. 파라미터 확장
   - ex) $var or ${var}
2. 명령 대체
   - $(command)
3. 산술 확장
   - $((expression))



#### 3) 큰 따옴표 (double quotes)

- 텍스트가 여러 단어나 인수로 분리되지 않도록 보호
- 큰 따옴표 내 문자들을 대체하는 것이 가능
  - \\(백 슬래시), $(달러), `(백틱) 을 제외한 대부분의 특수 문자는 일반 문자로 해석됨



#### 4) 작은 따옴표 (single quote)

- 문자 그대로의 의미를 갖도록 텍스트 보호
- 모든 특수문자의 해석이 방지됨



#### 5) escape

> \\

- 다음 문자가 특수 문자로 해석되는 것을 방지
- 큰 따옴표 안에서 작동, 작은 따옴표에서는 무시



#### 6) 주석 (comment)

> #

- '#' 문자를 쓰면 그 행의 끝까지 모두 주석 처리
- 쉘에 의해 처리되지 않음



#### 7) 테스트 (test)

> [[]]

- 조건부 표현식이 true인지 false 인지 결정하기 위한 조건식의 평가



#### 8) 부정 (negate)

> !

- 테스트나 종료 상태를 무효화하거나 되돌리기 위해 사용



#### 9) 방향재지정 (redirection)

> \><

- 명령의 입출력을 재지정



#### 10) pipe

> |

- 초기 명령의 출력을 2차 명령의 입력으로 재지정
- 명령을 하나로 묶음



#### 11) 명령 분리자 (command separator)

> ;

- 같은 줄에 있는 여러 명령을 구분



#### 12) 인라인 그룹

> {}

- 중괄호 안의 명령은 하나의 명령처럼 취급
- bash 구문이 하나의 명령만을 필요로 하고 함수의 사용은 피하고 싶을 때 사용하면 편리



#### 13) 서브 셸 그룹

> ()

- 내부 명령이 서브 쉘에서 실행되는 경우



#### 14) 산술 표현식

> (())

- 변수 할당이나 테스트에도 사용 가능
  - ex. ((a=1+4)) / if ((a<b))
  - \



#### 15) 산술 확장

> $(())

- 산술 표현식과 유사, 산술 계산 결과로 대체됨

```
$ echo "The average is $(( (a+b)/2 ))"
```



#### 16) 홈 디렉토리

> ~



## 6. 쉘 변수

- 변수 선언 시 '=' 양쪽에 공백 문자가 있으면 안 됨
- 변수 사용 시 앞에 '$' 문자를 붙여야 함

```
$ animal=tiger

# 오류
$ animal =tiger
$ animal= tiger

$ color=white
$ echo "tiger's color is $color"
tiger's color is white
```



## 7. 파라미터 대체와 인용부호

- 변수에 공백이 포함되어 있어 인용부호("")를 붙여야 함

```
$ book="The old man and the sea.mp3"

# 에러
$ rm $book

# 정상
$ rm "$book"
```

- 파라미터 구분을 위해 {} 기호를 써줌

```
$ animal=Tiger; color=Red

# 의도=Tigers Reds => 아무것도 출력되지 않음
$ echo "$animals $colors"

# 정상동작
$ echo ${animal}s vs. ${color}s
Tigers vs. Reds

# 확실하게 하려면 인용부호("") 붙이기
$ echo "${animal}s vs. ${color}s"
Tigers vs. Reds
```



## 8. 특수 매개변수

- ` (backtick) 백틱 사이 실행이 먼저 됨

```
$ vim whereis.sh

#!/bin/bash
DIRECTORY=`dirname $0`
echo $DIRECTORY

# "dirname $0" 실행 후 DIRECTORY 변수에 대입
$ chmod +x whereis.sh
$ ./whereis.sh
.
```



- 파일 실행 시 전달인자 사용

```
$ vim whois.sh

#!/bin/bash
name=$1
email=$2
all=$*

echo "your name is $name"
echo "your email is $email"
echo "* is $all"

$ ./whois.sh
your name is
your email is
* is

# $1=./whois.sh $2=gildong $3=gildong@gmail.com
$ ./whois.sh gildong gildong@gmail.com
your name is gildong
your email is gildong@gmail.com
* is gildong gildong@gmail.com
```



#### 특수 매개변수

| name    | usage  | description                                                  |
| ------- | ------ | ------------------------------------------------------------ |
| 0       | $0     | 스크립트의 이름 또는 경로 포함                               |
| 1 2 etc | $1 etc | 현재 스크립트 또는 함수에 전달된 인수                        |
| *       | "$*"   | 모든 위치 매개변수의 모든 단어, 큰따옴표를 붙이면 IFS 변수의 첫번째 문자로 분리된 모든 문자열을 포함하는 단일 문자열 |
| @       | $@     | 모든 위치 매개변수의 모든 단어                               |
| #       | $      | 위치 매개변수의 수                                           |
| ?       | $?     | 가장 최근에 완료한 포그라운드 명령의 종료 코드               |
| $       | $$     | 현재 쉘의 PID                                                |
| !       | $!     | 백그라운드에서 가장 최근에 실행된 명령의 PID                 |
| _       | $_     | 실행된 마지막 명령의 마지막 인수                             |



