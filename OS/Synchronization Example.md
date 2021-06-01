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