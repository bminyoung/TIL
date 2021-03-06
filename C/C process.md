﻿# C 프로그램 개발

## 1. Code 작성
> 코드 편집기나 텍스트 편집기로 C의 문법에 맞추어 소스코드를 작성한다.

## 2. 전처리기
> 컴파일 전에 실행된다.

- #include
- #define
- #ifdef, #ifndef / #endif
- ...

## 3. Compile
> C언어의 문법에 맞지 않으면 컴파일 에러를 발생시킨다.
> 컴파일 에러가 발생하지 않으면 오브젝트 파일(.o)을 생성한다.
> 소스 파일마다 오브젝트 파일이 각각 생성된다.

## 4. Link
> 컴파일 후 생성된 오브젝트 파일들을 합쳐서 한 개의 실행파일을 만든다.
> 사용된 라이브러리를 실행파일에 연결(link)하기도 한다.

- 라이브러리 연결 시 링크 에러가 발생할 수 있는데, 이를 해결하기 위해 파일 간 관계를 파악해야 한다.
	- 컴파일 에러보다 해결하기 어렵다.


## 5. Execute
> 링크 결과 생성된 프로그램을 실행한다.

## 6. Debugging
> 프로그램이 원하는 결과를 내놓거나 실행 중 프로그램이 죽는 등의 문제가 발생할 수 있다. 디버깅 과정을 통해 이를 해결한다.

## C 프로그램 작성 및 개발
### 1. UNIX/Linux
- gcc 같은 컴파일러를 이용해서 컴파일 및 링크 수행

### 2. Windows
- IDE를 주로 사용
	- ex) C++ Builder, Visual C++
- 소스코드 작성, 컴파일, 링크, 실행, 디버깅을 모두 처리할 수 있다.