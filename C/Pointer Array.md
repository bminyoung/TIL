# Pointer Array

## 1. 포인터 배열
> [데이터형]* [배열명][배열크기]
```c
int* arr[3];
```
|arr[0]|arr[1]|arr[2]|
|---|---|---|
|int*|int*|int*|

- 배열의 원소(포인터)가 가리키는 int 값에 접근하려면 *를 사용한다.


#### int* 형 변수
1) int 값을 가리키는 변수일 수 있다.
2) int 배열의 특정한 원소를 가리키는 변수일 수 있다.

```c
// 1)
int x = 1, y = 3, z = 10;
int* arr[3] = {&x, &y, &z};
int i;
for(i = 0; i < 3; i++){
	//int값에 접근하려면 * 사용
	printf("%d ", *arr[i]);
}
```

```c
// 2)
int x[3] = {1,2,3};
int y[3] = {4,5,6};
int z[3] = {7,8,9};
int* arr[3] = {x, y, z};
for(i = 0; i < 3; i++){
	printf("%d ", arr[i][j]);
	// 1.배열에 접근 => arr[i]
	// 2.배열의 원소 => (arr[i])[j] = *(arr[i]+j)
	// ★ arr[i] 가 포인터변수
}
```

## 2. 구조체 배열
```c
typedef struct _student{
	char name[10];
	int kor_score;
	int math_score;
	int eng_score;
}student;
```
> 학생들의 리스트를 만들고 싶다. 몇명인지 모르므로 적당히 크기는 100으로 잡는다.    
> `student students[100];`    
> student 구조체의 크기가 100, 1000, ...이라면?
> => 메모리 낭비

- 대신 구조체 포인터 배열을 사용할 수 있다.
	- 포인터 변수의 크기는 4바이트로 고정

```c
student s1 = {"gildong", 80, 90, 70};
student s2 = {"younghee", 10, 20, 30};
student* students[] = {&s1, &s2};

int i;
for(i = 0; i < 2; i++){
	printf("name = %s\n", students[i]->name);
	printf("score = %d %d %d\n", students[i]->kor_score, students[i]->math_score, students[i]->eng_score);
	//students[i] = 포인터 변수
```
- `student* students[] = {&s1, &s2}` : 배열에 지역변수 s1, s2의 주소를 대입해주었다 => 보통 지역변수가 아닌 동적메모리를 사용한다. [동적메모리 할당 ](./malloc.md) 참조