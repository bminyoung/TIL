# Process managing

### Process ID
> 프로세스를 구분하는 유일한 식별자 (=pid)

## 1. 프로세스 계층
- 부모 : 새 프로세스를 띄우는 프로세스
- └ 자식 : 새로운 프로세스

- 모든 프로세스는 부모를 가진다
	- 부모의 pid = ppid

- 프로세스 ID는 pid_t 타입으로 표현된다. 이는 <sys/types.h> 헤더에 정의되어있다.
- pid_t는 C의 int 타입으로 정의한다.

#### pid, ppid 얻기
> pid_t getpid(void)
> pid_t getppid(void);


```c
#include <sys/types.h>
#include <unistd.h>

printf("pid= %d\n", getpid());
printf("ppid= %d\n", getppid());
```

## 2. exec
> 새로운 프로그램을 실행하는 기능은 exec 호출 군이 제공한다.

- 새로운 프로세스를 실행하기 위해 부모 프로세스를 복제한다. (=fork)
- 새로운 프로그램을 새로운 프로세스에 올려 실행하는 작업
	- => fork(프로세스를 만든다) -> exec(새 이미지를 프로세스에 올린다)