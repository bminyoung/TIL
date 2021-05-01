# 윈도우에서 리눅스 사용
> 컴파일 전에 실행된다.

- #define, #include, #if, #else, ...

## 1. GNU 툴체인 설치

```
# 패키지 리스트 업데이트
> sudo apt-get update

# gcc, g++, gdb 설치 (build-essential: gcc, g++)
> sudo apt-get install build-essential gdb

> gcc --version
> g++ --version
> gdb --version
```



## 2. VS code (optional)
### 1) VS code 설치
### 2) WSL 확장팩 설치

- [확장] - [검색] - "remote" 검색
- "Remote - WSL" 확장팩 설치

### 3) VS code에서 WSL 연결

- 좌측 하단에서 "원격 창 열기"
- "Remote - WSL: New Window" 선택
- 폴더 열기 - 홈 디렉토리가 열림 - 새 디렉토리 만들고 연결



## 3. Example in vscode

```c
// hello.c (install c/c++ extension)
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
    pid_t pid;
    pid = fork();
    printf("Hello, WSL!\n");

    return 0;
}
```

- [Terminal] - [New Terminal]

```
> gcc hello.c
> ./a.out
```