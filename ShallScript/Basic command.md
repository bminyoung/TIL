# Basic Command
## 1. echo
> 문자열 프린트
>
> echo [출력할 문자열]

```
$ echo hello world
hello world

# 공백문자는 1개로 취급됨
# 단어와 단어 / 명령과 옵션 / 전달인자를 구분하는 용도
$ echo hello    world
hello world

# 인용부호 내 공백문자는 문자로 취급
$ echo "hello    world"
hello    world

$ echo 'hello world\n\n\n'
hello world\n\n\n

$ echo -e 'hello world\n\n'
hello world
(줄바꿈)
(줄바꿈)

# 비프음
$ echo -e '\a'
$ echo $'\a'

# -n 옵션: 줄바꿈 처리가 안됨
$ echo -n 'hello world'
hello worlduser@linux$

# 파일 목록 출력 (공백문자로만 구분, substring시 유용)
$ echo *

```



## 2. 테스트

> [ 테스트할 내용 ]
>
> '[' 와 ']' 는 띄어쓴다.

```
# test.txt 파일이 있는지 확인
$ [ -f 'test.txt' ]
```

- -e: 파일이 존재하는지
- -f: 일반 파일인지
- -b: 블록 파일인지
- -d: 디렉토리인지



## 3. alias

> 별칭
>
> 긴 명령어를 단축명령어로 쓸 수 있음

```
# h 입력 시 history 입력과 같은 결과
$ alias h='history'
```


- alias의 한계 -> function 사용

```
# test1, test2, test3, ...
$ alias t1='/test/test1'
$ alias t2='/test/test2'

$ function ttest() { /test/test${1}; }
$ ttest 1
$ ttest 2
```



## 4. pushd, popd

> 원하는 경로 저장/불러오기 (= cd -)

```
# 현재 경로 저장
$ pushd .
~/Desktop ~/Desktop

# 저장한 경로로 이동
$ popd
~/Desktop
```



## 5. printf

> 형식화된 출력

```
$ printf "%02d" 1
01

$ printf "%05d\n" 1
00001

# legend 라는 변수에 "$name jackson" 값이 들어감
$ name=michael; printf -v legend "%s jackson" $name; echo $legend
michael jackson
```

- 변수 선언: [변수]=[값] (공백 없이)
- 변수 참조: $[변수]



## 6. read

>사용자로부터 입력을 받음

```
$ read num
12345
# => num이라는 변수에 12345 저장

$ echo $num
12345


$ read -p "what is your phone number" v
what is your phone number010-1234-5678
# => v라는 변수에 저장

$echo -v
010-1234-5678


# -n 1 : 문자 1개만 입력받음 (엔터 필요없음)
$ read -n 1 -p "Are you over 16?" v
Are you over 16?y

# -s : 사용자의 입력값이 화면에 나타나지 않음
$ read -s -n 1 -p "Are you over 16?" v
Are you over 16?

# -t 3 : 3초동안 입력 시간을 제한
$ read -s -n 1 -t 3 -p "Are you over 16?" v
Are you over 16?


```



## 7. while..do..done

> 명령어 반복
>
> while .. [조건] .. do .. [조건이 참일 경우 실행할 문장] .. done

```
$ no=1; while (( no < 10 )); do printf "%02d\n" $no; ((no++)); done
01
02
03
04
05
06
07
08
09
```

