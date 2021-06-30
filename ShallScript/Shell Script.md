# Shell Script

## 1. Shell Script
> 명령 인터프리터 (Command interpreter)

- 사용자가 OS에 **대화식**으로 명령을 내리거나 **일괄**적으로 실행할 수 있는 기능을 제공하는 응용 프로그램
- 사용자가 시스템과 대화할 수 있는 방법

- 커널: OS의 코어부분, 하드웨어를 운영
  - 사용자나 응용 프로그램에 시스템 제반 기능을 서비스 형태로 지원

- 쉘: OS의 중심부
  - 사용자와 상호작용
  - 요구사항을 커널로 전달



## 2. 작성 방법

- 파일 맨 앞에 `#!/bin/bash` 입력: 쉬뱅(해시뱅)
  - /bin/bash 가 주된 실행자

```
<hello world.sh 파일>
#!/bin/bash
echo hello world
```



- /bin/bash가 없어도 (bin에 bash가 없어도) 실행 가능

```
<hello world.sh 파일>
#!/usr/bin/env bash
echo hello world
```



