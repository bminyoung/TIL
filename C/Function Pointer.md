# Pointer of function

## 1. 프로그램 영역
- 컴파일, 링크 후에 실행 파일이 만들어진다.
- 실행 파일에는 코드영역, 데이터 영역이 있다.
	- 코드 영역 : 변수(지역, 전역) 등 할당
	- 데이터 영역 : 함수 등 할당
- 함수도 주소를 가진다. -> 포인터에 저장, 사용이 가능

## 2. 함수에 대한 포인터
> [리턴타입] (*포인터변수명)(매개변수)

```c
int add(int num1, int num2);
...
// &add 를 대입해도 됨
int (*func)(int a, int b) = add;

//사용
int ret;
ret = func(1, 2); //포인터 변수(func)를 함수명인 것처럼 사용할 수 있다.
ret = (*func)(10, 20);
ret = *func(10, 20); // error! *(func(10, 20)) 와 같은 뜻
```

## 3. 함수에 대한 포인터 형식 정의
- typedef를 이용한다.
>  typedef [리턴형] (*포인터형식명)(매개변수)

- 함수 이름은 마음대로 지정할 수 있으나 함수의 원형은 정해진대로 지켜야한다.
```c
typedef int (*myfunc)(int n1, n2);
int add(int a, int b); //위의 원형을 지켜야한다.
void testprint(int a, int b, *myfunc func){ //for test
	int res = func(a, b);
	printf("result= %d\n", res);
}
...
myfunc func = add;
testprint(1, 2, func);

/* 다음 내용이 출력된다.
 * result= 3
 */
```

