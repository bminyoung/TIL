# Compare&Loop
## 1. 조건문

> if ... else ... fi

- if 다음 : 산수, 테스트 모두 가능

```
$ if true; then
> echo true
> else
> echo false
> fi
true

$ if true; then echo true; else echo false; fi
true
```

- 스타일

```
# 스타일 1
if commands
then other commands
fi

# 스타일 2
if commands
then
other commands
fi

# 스타일 3
if commands; then
other commands
fi
```



## 2. [..] vs [[..]]

- [] : 테스트에 사용
- [] 안에 >< : 리다이렉션의 의미

```
$ tom="Tom hanks"
$ deniro="Robert Deniro"
$ [ $tom > $deniro ]

# 수정
$ [[ $tom > $deniro ]]
$ echo $?
0

# 아래 두 명령은 같음
$ [ $tom = $deniro ]
$ [ Tom hanks = Robert Deniro ]

# 수정
$ [ "$tom" = "$deniro" ]
$ [[ $tom = $deniro ]];echo $?
1
```

- 인용부호 사용 시 주의

```
# 아래 두 명령은 같음 (if 다음 조건 좌항이 빔)
$ VAR=; if [ $VAR = "" ];then echo true; else echo false;fi
$ VAR=; if [  = "" ];then echo true; else echo false;fi

# 수정 => 인용부호 사용 or [[]] 사용
$ VAR=; if [ "$VAR" = "" ];then echo true; else echo false;fi
true
$ VAR=; if [[ $VAR = "" ]];then echo true; else echo false;fi
true
```



## 3. 비교 메타 문자열

| name    | desc                               |
| ------- | ---------------------------------- |
| -e FILE | 파일이 있으면 true                 |
| -f FILE | 파일이 일반 파일이면 true          |
| -d FILE | 파일이 디렉터리면 true             |
| -h FILE | 파일이 심볼 링크면 true            |
| -p PIPE | 파이프가 있으면 true               |
| -r FILE | 파일을 읽을 수 있으면 true         |
| -s FILE | 파일이 존재 & 비어있지 않으면 true |
| -t FD   | 터미널에서 FD가 열려있으면 true    |
| -w FILE | 파일을 쓸 수 있으면 true           |



```
# "hello.txt.bak" 가 존재하지 않으면 "hello.txt" 복사
$ if [ ! -f "hello.txt.bak" ]; then
> cp "hello.txt" "hello.txt.bak"
> fi

# 전달인자를 입력하지 않았거나 쉘의 요구사항을 만족하지 않았을때 사용
$ if (( $? )); then
> echo 'Plz run using "bash" or "sh", but not "." or "source"' >&2
> exit 1
> fi
Plz run using "bash" or "sh", but not "." or "source"
exit

# 파일 존재 여부 확인
$ if [[ $(ls -A) ]]; then
> echo "there are files"
> else
> echo "no files found"
> fi
there are files

# -ge : g(greater)+e(equal)
$ ./sleep.sh &
$ result=`ps aux | grep -i "sleep.sh" | grep -v "grep" | wc -l`
$ if [ $result -ge 1 ]
> then
> echo "script is running"
> else
> echo "script is not running"
> fi
script is running
```

- 파일 비교

| name            | desc                                  |
| --------------- | ------------------------------------- |
| -x FILE         | 파일이 실행 가능이면 true             |
| -O FILE         | 파일이 사용자가 소유하는 경우 true    |
| -G FILE         | 파일이 그룹에 의해 소유되는 경우 true |
| FILE1 -nt FILE2 | FILE1이 FILE2보다 최신이면 true       |
| FILE1 -ot FILE2 | FILE1이 FILE2보다 오래된 경우 true    |

- 문자열

| name              | desc                                     |
| ----------------- | ---------------------------------------- |
| -z STRING         | 문자열이 비어있으면  true                |
| -n  STRING        | 문자열이 비어있지 않으면  true           |
| STRING = STRING   | 문자열이 같으면 true                     |
| STRING != STRING  | 문자열이 다르면 true                     |
| STRING1 < STRING2 | STRING1이 사전 순서로 먼저 나오면 true   |
| STRING1 > STRING2 | STRING1이 사전 순서로 나중에 나오면 true |

- 수 비교

| name          | desc                           |
| ------------- | ------------------------------ |
| EXPR -a EXPR  | 두 식 모두 true면 true         |
| EXPR -o EXPR  | 두 식 중 하나라고 true 면 true |
| ! EXPR        | 식의 결과 반전 (not)           |
| INT -eq INT   | 두 수가 같으면 true            |
| INT -ne INT   | 두 수가 다르면 true            |
| INT1 -lt INT2 | INT1 < INT2 면 TRUE            |
| INT1 -gt INT2 | INT1 > INT2 면 TRUE            |
| INT1 -le INT2 | INT1 <= INT2 면 TRUE           |
| INT1 -ge INT2 | INT1 <= INT2 면 TRUE           |

- [[]]을 사용, [] 보다는 [[]]를 사용하는 것이 좋음

| name                    | desc                                                         |
| ----------------------- | ------------------------------------------------------------ |
| STRING =(or ==) PATTERN | 패턴이 일치하면 true                                         |
| STRING != PATTERN       | 패턴이 일치하지 않으면 true                                  |
| STRING =~ REGEX         | regex 패턴과 일치하면 true                                   |
| ( EXPR )                | 평가 우선순위 변경                                           |
| EXPR && EXPR            | 테스트 -a와 유사, 첫 식이 거짓이면 두번째 식은 고려하지 않음 |
| EXPR \|\| EXPR          | 테스트 -o와 유사, 첫 식이 참이면 두번째 식은 고려하지 않음   |



#### [실습] 전달인자를 입력하지 않았을 때 안내문 출력

```
#!/bin/bash

if [ -z "$1" ]; then
	echo "usage:$0 directory"
	exit
fi
echo 'Have a nice day!'
```

























