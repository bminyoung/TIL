﻿# Stream

## 1. 스트림
> 연속된 데이터 바이트의 흐름

#### 스트림 기반 입출력의 장점
- `장치 독립성`
	- 입출력 장치 종류와 상관없이 같은 방법으로 입출력을 수행할 수 있다.
- `속도`
	- 입출력장치는 CPU에 비해 속도가 느리다. => CPU가 입력을 기다리는 것은 비효율적
	- 입력 스트림에 버퍼를 두고 입력된 내용을 버퍼에 저장했다가 한번에 전달

## 2. 표준 입출력
### 1) 출력
> int printf(const char* format [, argument]... );

- 가변 인자를 갖는다.

### 2) 입력
> int scanf(const char* format [, argument]... );

- 정상적으로 입력된 항목의 개수를 리턴한다.
```c
int x, y;
int res = scanf("%d %d", &x, &y);
if(res < 2) printf("잘못 입력함\n");
```