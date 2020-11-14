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