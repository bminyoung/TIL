# Synchronization Examples

## 1. 고전적인 동기화 문제

#### 1) 유한 버퍼 문제

- 생산자와 소비자가 자료구조를 공유함

  - ```
    # n개의 버퍼로 구성된 풀
    int n;
    semaphore mutex = 1; //이진 세마포
    semaphore empty = n; //비어있는 버퍼 개수
    semaphore full = 0; //채워져있는 버퍼 개수
    ```

    

- 생산자 프로세스 구조
  - <img src="./Image/producer process.jpg" alt="producer process" style="zoom:80%;" />
  
- 소비자 프로세스 구조
  - <img src="./Image/consumer process.jpg" alt="consumer process" style="zoom:80%;" />

- 생산자는 버퍼를 채우면서 full++

- 소비자는 버퍼를 비우면서 empty--

- mutex는 버퍼 풀에 접근하기 위한 상호 배제 기능을 제공함



#### 2) Readers-Writers 문제

- Reader : DB를 읽는 등 데이터를 읽는 프로세스(or 스레드)

- Writer : DB를 갱신하는 등 데이터를 쓰는 프로세스(or 스레드)

- 2개의 writer가 동시에 접근하면 문제가 생길 수 있음

  => Readers-Writers 문제 (writer의 쓰기 작업 동안 공유데이터에 배타적 접근 권한을 부여)
  
- 두가지 유형

  1. writer가 공유객체 사용 허가를 얻지 못했으면, 어느 reader도 기다리게하면 안됨

     => writer가 기아 상태에 빠질 수 있음

  2. writer가 준비되면 새로운 reader는 읽기를 시작하지 못함

     => reader가 기아 상태에 빠질 수 있음

##### 1번 유형에 대한 해결

```
semaphore rw_mutex = 1; //이진 세마포
semaphore mutex = 1; //이진 세마포
int read_count = 0;
```

- **mutex**: read_count 갱신 시 상호 배제 보장
- **read_count**: 몇 개의 프로세스들이 객체를 읽고 있는지
- **rw_mutex**: writer들을 위한 상호 배제 세마포, 임계구역에 진입하는 첫 reader & 빠져나오는 마지막 reader도 사용
- writer process
  - <img src="./Image/writer process.jpg" alt="writer process" style="zoom:80%;" />
- reader process
  - <img src="./Image/reader process.jpg" alt="reader process" style="zoom:80%;" />

- 1개의 reader 만이 rw_mutex 관련 큐에 들어감

- writer가 signal(rw_mutex) 실행 시 (n개의 reader) or (1개의 writer)의 수행 재개

  (스케줄러가 결정)

- read-writer 락: Readers-writers 문제 & 해결안을 일반화하여 몇몇 시스템에서 제공

  - 읽기 or 쓰기 모드 지정
  - 쓰기 모드는 하나의 프로세스만 획득 가능

- read-writer 락이 유용한 상황

  - 공유 데이터를 읽기만 or 쓰기만 하는 스레드를 식별하기 쉬운 프로그램
  - (#writer ) < (#reader): read-writer 락을 설정하는 데에 오버헤드가 비교적 크게 듦(세마포, 상호 배제 락보다) -> 여러 reader가 읽게 해서 병행성을 높임으로 상쇄

#### 3) 식사하는 철학자들 문제

> 원형 테이블에 앉은 5명의 철학자들
>
> 각 철학자들 양쪽에는 젓가락 한쪽씩
>
> 양쪽의 젓가락을 집으면 식사 시작, 식사가 끝나면 젓가락을 놓음

