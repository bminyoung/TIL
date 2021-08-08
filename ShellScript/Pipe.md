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



## 4. 함수

> 함수명() {}
>
> function 함수명() {}

- 소괄호 내에 아무것도 적지 않음
- 선 정의 후 사용

- 재사용성 증가
- 가독성 증가

```
$ sum() { declare -i sum; START=$1; END=$2;for i in `eval echo {$START..$END}`; do ((sum+=i)); done; echo $sum; }

$ total=$(sum 1 100); echo $total
5050
```



## 5. shift

>매개변수 리스트를 하나씩 자리이동

```
$ set 1 2 3 4 5
$ while [$# -gt 0 ]; do echo $1; shift 1;done
1
2
3
4
5
```



## 6. source, bashrc

> source : bashrc의 내용을 적용시킴
>
> source ~/.bashrc
>
> 또는 . ~/.bashrc

```
$ source ~/.bashrc
$ . ~/.bashrc

# 그냥 실행 시 오류
$ ~/.bashrc
Permission denied
```



## 7. 작업제어

- 모든 프로세스(프로그램)는 모든 입/출력 오류 장치(파일)를 **오픈**한 상태로 실행
  - STDIN / STDOUT / STDERR
- ctrl + c : 인터럽트
- ctrl + z : 프로세스 일시정지
- bg : 가장 최근의 프로세스 백그라운드화
- fg : 가장 최근의 프로세스 포그라운드화

```
# foreground process
$ sleep 1000

# background process
$ sleep 1000 &

# background -> foreground
$ fg
```



