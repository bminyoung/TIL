# Pipe
## 1. 파이프

- 파이프의 읽기 끝 / 쓰기 끝
  - 쓰기 쪽에 기록된 데이터는 읽기 쪽에서 읽을 수 있음
- 프로세스가 파이프에 쓰기를 시도하는 경우 다른 프로세스가 파이프에서 충분히 데이터를 읽을 때까지 쓰기 동작이 끝나지 않고 **블록**됨

```
# mknod : 특수한 장치 파일을 만들 때 사용
$ mknod /tmp/mypipe p
$ echo hello world >/tmp/mypipe
# 블록상태

### 다른 프로세스
# 파이프에서 읽기 동작 -> 위의 블록 상태가 풀림
$ cat /tmp/mypipe
```

- | (파이프) : 가장 주된 용도

```
$ cat hello.txt | more
hello

$ find . -name "*.o" -print0 | xargs -0 rm -rf
```



