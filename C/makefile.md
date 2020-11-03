# makefile
> makefile 을 이용하면 컴파일이 편리해진다.

- 파일 간 관계를 파악하기 쉽다.
- 반복 작업을 최소화할 수 있다.

#### makefile 이용x
```
(컴파일)
gcc -c -o test.o test.c
gcc -c -o main.o main.c
(링크)
gcc -o main.out main.o test.o
```
- 명령어를 한 줄 한 줄 입력해야한다.

#### makefile 사용
```
[makefile]
gcc -c -o test.o test.c
gcc -c -o main.o main.c
gcc -o main.out main.o test.o
```
- 콘솔에서 `make` 입력하면 컴파일된다.

## makefile 작성
```
[target] : [dependency]
(tab)[Recipe]
```
- target : 명령어의 결과로 생성되는 파일
- dependency : target을 생성할 때 의존하는 파일들
- recipe : target을 생성하는 명령 (tab을 해주어야 한다)