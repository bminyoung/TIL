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



