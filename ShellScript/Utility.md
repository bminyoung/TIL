# Utility
## 1. nohup

> 로그아웃 or 터미널 종료 후에도 명령이 계속 실행됨 (데몬화)

```
# 강제 종료 시 (ex. ctrl+c) sleep 명령어도 종료됨
$ sleep 1000
```

- 예제

```
# mydaemon.sh 파일

#!/bin/bash

for i in{1..60};do
date >> mydaemon.log
sleep 1
done
```

```
$ date;nohup ./mydaemon.sh 1>/dev/null 2>&1 0</dev/null &
```

- 1>/dev/null : 표준 출력은 휴지통으로
- 2>&1 : 표준 에러는 표준 출력으로
- 0</dev/null : 표준 입력을 차단
- & : 백드라운드 프로세스 화

