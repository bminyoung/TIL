# File I/O

## 0. File I/O 순서
1. 파일 열기 : fopen
2. 입출력 : fprintf, fscanf, fread, fwrite, ...
3. 파일 닫기 : fclose

## 1. 파일 열기
> FILE* fopen(const char* filename, const char* mode)

- filename : 파일명, mode : 파일 열기 모드
- 리턴값 : 파일 포인터, 실패 시 NULL 포인터
- 파일 열기 모드
|모드|뜻|
|---|---|
|r|읽기 전용(파일 없으면 실패)|
|w|쓰기 전용(파일 없으면 생성, 있으면 덮어쓰기)|
|a|파일의 끝에 쓰기(파일 없으면 생성, 쓰기는 끝에만 가능, 읽기는 제한x)|
|r+|읽고 쓰기 가능(파일 없으면 실패)|
|w+|읽고 쓰기 가능(파일 없으면 생성, 있으면 덮어쓰기|
|a+|읽고 쓰기 가능(파일 없으면 생성, 쓰기는 끝에만 가능, 읽기는 제한x)|
|t|텍스트 모드|
|b|바이너리 모드|

## 2. 파일 닫기
> int fclose(FILE* stream)

- 파일 입출력 후 파일을 꼭 닫아주어야 한다.