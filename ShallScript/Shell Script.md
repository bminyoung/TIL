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



## 3. DOS스타일의 줄끝

- LF: Line Feed
- CR: Carriage Return
- linux: LF
- windows: CRLF
- 쉘에서 동작하는, 리눅스에서 사용하는 파일은 windows의 편집기는 피할 것



## 4. 실행 방법

```
# 실행 권한 주기
$ chmod +x helloworld.sh

# 1. 경로
$ ./helloworld.sh
hello world

# 2. bash
$ bash helloworld.sh
hello world

# 3. source
$ source helloworld.sh
hello world

# 4. dot
$ . helloworld.sh
hello world
```



## 5. 특수문자

#### 1) 공백 (white space)

- 탭, 줄 바꿈, 세로 탭, 양식 공급, 캐리지 리턴 또는 공백
- bash는 공백을 사용하여 단어의 시작, 끝을 결정
- 명령어 입력 시 첫번째 단어는 **명령 이름**, 추가 단어는 해당 명령에 대한 **인수**



#### 2) 확장 (expansion)

- 다양한 유형의 확장을 도입

1. 파라미터 확장
   - ex) $var or ${var}
2. 명령 대체
   - $(command)
3. 산술 확장
   - $((expression))