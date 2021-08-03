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



## 2. 프로세스 대체

> \<(명령어)

- 프로세스 대체 : 코드의 가독성이 좋아짐

```
# comm : 두 개의 디렉토리의 차이점을 확인할 때 유용
# 2 : 2번째 폴더의 파일은 출력x / 3 : 공통 파일은 출력x
$ comm -23 <(ls -R 경로|sort) <(ls -R 경로2|sort)
```

- while 안으로 명령 대체 전달
- jpg 파일의 개수 구하기

```
# find 이하 명령대체가 먼저 실행, 결과를 while 안으로 전달
$ while read file; do
> ((i++))
> done < <(find . -type f -name "*.jpg")

$ echo $i
```



## 3. 서브 쉘

> (명령)

```
# 20초간 파일에 write
$ echo begin;(for i in {200..220}); do echo $i >> num100; sleep 1;done)&

# test폴더의 파일을 익명(-)파일로 압축 -> Desktop으로 이동해 압축 풀기
# 복사 시간이 짧아짐
$ (cd ~/Desktop/test && tar cf - .) | (cd ~/Desktop && tar xpvf -)
```













