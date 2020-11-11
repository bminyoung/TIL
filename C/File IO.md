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

## 3. 텍스트 파일 입출력

#### fgetc
- 파일에서 한 글자를 입력받는다.
> int fgetc(FILE *fp)

```c
FILE* fp = fopen(argv[1], "r");
char ch;
while( (ch = fgetc(fp)) != EOF){
	printf("%c",ch);
}
printf("\n");
fclose(fp);
```

#### putchar
- 파일에 한 글자를 출력한다.
> int putchar(int c, FILE *fp)

```c
FILE* fp = fopen(argv[1], "w");
char ch;
while( scanf("%c", ch) == 1){
	fputc(ch, fp);
}
fclose(fp);
```


#### fgets
- 파일에서 한 줄을 입력받는다.
> char *fgets(char *str, int n, FILE *stream

#### fputs
- 파일에서 한 줄을 출력한다.
> int fputs(const char *str, FILE *fp)


#### fscanf
- 파일에서 형식 문자열을 이용해 입력받는다.
> int fscanf(FILE *fp, ...)

#### fprintf
- 형식 문자열을 이용해 파일에 출력한다.
> int fprintf(FILE *fp, ...)
