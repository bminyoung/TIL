﻿# Daemon
> 배경으로 동작하는 프로세스

### 요구사항
1. init 의 자식 프로세스로 동작할 것
2. 터미널에 연결하면 안 됨

## 1. 데몬이 되기 위한 단계
1) fork() : 새로 데몬이 될 프로세스를 만든다.
2) 부모 프로세스에서 exit() 호출