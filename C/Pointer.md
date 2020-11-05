# Pointer

## 1. 포인터 배열
> [데이터형]* [배열명][배열크기]
```c
int* arr[3];
```
|arr[0]|arr[1]|arr[2]|    
|---|---|---|    
|int*|int*|int*|

- 배열의 원소(포인터)가 가리키는 int 값에 접근하려면 *를 사용한다.
```c
int x = 1, y = 3, z = 10;
int* arr[3] = {&x, &y, &z};
int i;
for(i = 0; i < 3; i++)
	printf("%d ", *arr[i]);
```