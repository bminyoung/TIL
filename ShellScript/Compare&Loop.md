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



## 4. 반복문

> while [테스트 코드]; do ... done
>
> for [범위]; do ... done

```
# "hello world"를 지속적으로 출력
$ while true; do
> echo "hello world"
> sleep 1
> done

# 비프음을 지속적으로 출력
$ while true; do
> echo -n -e "\a";
> sleep 1;
> done

# 1~10 출력 (중괄호 확장을 위해 eval 사용)
$ COUNT=10
$ for no in `eval echo {0..$COUNT}`; do
> echo $no
> done

# 위와 같음
$ for no in 0 1 2 3 4 5 6 7 8 9 10; do
> echo $no
> done
```



#### [실습] 1~10의 합

```
$ sum=0
$ for no in {1..10}; do
> ((sum=sum+no))
> done
> echo SUM=$sum
SUM=55
```



> for .. in ..

```
# pen -> 빈 문자열로 만들기
$ classroom=(desk pen note chair book)
$ echo ${classroom[@]}
desk pen note chair book
$ for i in ${!classroom[@]} ; do
> 	if [ "${classroom[$i]}" = 'pen' ] ; then
> 		classroom[$i]=''
> 	fi
> done
$ echo ${classroom[@]}
desk note chair book
```

- ${!classroom[@]} -> ! : 배열의 인덱스 참조



> for ((;;)) 루프

```
# "Hello world" 문자열이 한글자씩 출력
$ mystr="Hello world"
$ for((i=0;i<${#mystr};i++)); do
>	c="${mystr:$i:1}"
>	echo "$c"
> done
```



#### [참조] date

```
$ date +"%Y-%m-%d"
2021-07-26

$ date +"%Y-%m-%d %r"
2021/07/26 10:30:43 PM

$ date +"%Y-%m-%d %H:%M %A"
2021/07/26 22:30 Monday

$ date "+DATE: %Y-%m-%d%nTIME: %H:%M:%S"
DATE: 2021-07-26
TIME: 22:30:43
```



#### [실습] 커맨드 시계

```
#!/bin/bash
while true; do
TIME=`DATE +'%Y-%m-%d %H:%M:%S'`
echo -ne "${TIME}\r"
sleep 1
done
```



## 5. 루프문과 glob

- glob 사용 시 인용부호를 사용하면 안됨

```
#########################
# 확장자가 mp3인 파일 삭제 #
#########################
$ cd mydir;ls
For Whom the Bell Tolls.mp3
Gone With the Wind.mp3

# 실패 -> "For" "Whom" "the" "Bell" 이런식으로 각각의 문자열로 인식됨
$ for file in $(ls *.mp3);do
>	rm "$file"
> done

# 실패 -> "For Whom the Bell Tolls.mp3 Gone With the Wind.mp3" 전체가 하나의 파일로 인식됨
$ for file in "$(ls *.mp3)"; do
> 	rm "$file";
> done

# 성공
$ for file in *.mp3
> do rm "$file"
> done
```

- rm "$file" : 인용부호를 써주어야함 (공백문자 때문)



#### [실습] 현재 폴더의 모든 파일의 백업파일 만들기

```
$ for file in *; do
> cp "$file"{,.bak}
> done
```



## 6. 명령어 seq

> 시퀀스 정의 및 출력

```
# 1 ~ 10
$ seq 1 10

# 0 2 4 6 8 10
$ seq 0 2 10

$ seq -s, 1 1 10
1,2,3,4,5,6,7,8,9,10

# 10 ~ 1
$ seq 10 -1 1
```



#### [실습] 형식화된 숫자 출력

```
$ for no in `seq 1 10`; do
> printf "%03d\t" $no
> done
```



## 7. case

> case .. in
>
> [경우 1] ) [명령];;
>
> [경우 2] ) [명령];;
>
> ...
>
> esac

- *) : 기타 (default)
- 세미콜론은 2개씩 적어야함 (세미콜론 하나는 명령어 구분)

```
$ read -p "Enter any string: "
Enter any string: abc
$ case $REPLY in
> 	+([[:digit:]]) ) echo "digits" ;;
>	*) echo "not digits" ;;
> esac
not digits
```



#### [실습] 사용자가 Y/N 입력

```
[case.sh]

#!/bin/bash
read -s -n 1 -p "You really want to exit? " response
case $response in
Y|y) echo YES;;
N|n) echo NO;;
*) echo Killed;;
esac
```



## 8. select

- 배열 요소가 메뉴 형식으로 출력되고 선택할 수 있음

```
$ movies=("Avengers" "Matrix" "Titanic")
$ PS3="Plz select your favorite movie: "
$ select movie in ${movies[@]}
> do
>	echo "$movie selected"
> done


$ movies=("Avengers" "Matrix" "Titanic" "None")
$ PS3="Plz select your favorite movie: "
$ select movie in ${movies[@]}
> do
>	case $movie in
>		"None") echo "not in list. quit";break;;
>		*) echo "$movie selected";;
>	esac
> done
```

















