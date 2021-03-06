﻿# Deadlock

> 교착상태
>
> 대기중인 프로세스가 요청한 자원들이 `다른 대기중인 프로세스`에 의해서 점유되어 있기 때문에 프로세스 상태를 변경시킬 수 없는 상태
>
> "두 기차가 교차로에서 서로 접근할 때, 둘 다 정지해야하며 상대방이 없어지지 않으면 누구도 다시 출발할 수 없음"

## 1. 시스템 모델

> 시스템은 경쟁하는 스레드에 분배돼야 할 유한한 자원들로 구성

- mutex, 세마포 등의 동기화 도구도 시스템 자원
  - 가장 일반적인 교착 상태의 발원지
- 프로세스의 자원 사용 순서
  1. **요청**: 자원을 요청, 바로 요청이 허용되지 않으면 대기함
  2. **사용**: 자원에 대한 작업을 수행
  3. **방출**: 자원을 방출



## 2. 다중 스레드 응용에서 교착 상태

```
# 스레드1
lock(mutex1)
lock(mutex2)
...
unlock(mutex2)
unlock(mutex1)

# 스레드1
lock(mutex2)
lock(mutex1)
...
unlock(mutex1)
unlock(mutex2)
```

- 스레드1이 mutex1획득, 스레드2가 mutex2를 획득하면 교착상태에 빠짐



#### 1) 라이브락

> 스레드가 실패한 행동을 계속해서 시도할 때 발생

- 예시: 복도에서 한 사람은 오른쪽, 한 사람은 왼쪽으로 움직이면 서로를 방해

  -> 한 사람은 왼쪽, 한 사람은 오른쪽으로 이동하면 여전히 서로를 방해 -> 반복 ...



## 3. 교착 상태 특성

#### 1) 필요조건

1. **상호 배제**: 한 번에 한 스레드만이 한 자원을 사용할 수 있다. 다른 스레드가 해당 자원을 요청하면 자원이 방출될 때까지 지연되어야 한다.
2. **점유하며 대기**: 스레드는 최소한 하나의 자원을 점유한 채, 현재 다른 스레드에 의해 점유된 자원을 추가로 얻기 위해 대기해야한다.
3. **비선점**: 자원들을 선점할 수 없어야 한다.
4. **순환 대기**: 대기하는 스레드 집합 {T_0, T_1, T_2, ... T_n} 에서 T_0는 T_1이 점유한 자원 대기, T_1은 T_2가 점유한 자원 대기, ... T_n은 T_0가 점유한 자원을 대기한다.

- 교착 상태가 발생하려면 위 4가지 조건을 만족해야 함



#### 2) 자원 할당 그래프

> 정점과 간선으로 이루어진 그래프, 교착 상태를 정확히 기술할 수 있음
>
> T: 활성 스레드 집합
>
> R: 자원 유형 집합
>
> T -> R: 요청 간선
>
> R -> T: 할당 간선

- 자원 할당 그래프에 사이클이 없으면 교착 상태가 **아님**
- 자원 할당 그래프에 사이클이 있으면 교착 상태인지 아닌지 **알 수 없음**
- 사이클이 있고 교착 상태인 그래프
  - <img src="./Image/cycle_deadlock.jpg" alt="deadlock" style="zoom:50%;" />
- 사이클이 있고 교착 상태가 아닌 그래프
  - <img src="./Image/cycle_nodeadlock.jpg" alt="nodeadlock" style="zoom:50%;" />

## 4. 교착 상태 처리 방법

>1. 교착 상태가 발생하지 않는 척
>2. 교착 상태를 예방하거나 회피하는 프로토콜 사용
>3. 교착 상태가 되도록 허용한 후 복구

- 교착 상태 예방: 교착 상태가 발생하기 위한 4가지 조건 중 적어도 하나가 성립하지 않게 보장
- 교착 상태 회피: 스레드가 평생 요구, 사용할 자원에 대한 부가 정보 요구



## 5. 교착 상태 예방

#### 1) 상호 배제

- 공유가 가능한 자원들은 배타적인 접근을 요구하지 않음 -> 교착 상태 x
  - ex) 읽기 전용 파일 (공유 가능한 자원)
- 공유가 불가능한 자원이 있어 상호 배제 조건을 거부, 교착 상태 예방은 불가능
  - ex) mutex 락

#### 2) 점유하며 대기

- 점유하며 대기 조건이 발생하지 않으려면 스레드가 자원을 요청할 때 다른 자원은 보유하면 안됨

  -> 실용적이지 않음

#### 3) 비선점

- 비선점 조건이 발생하지 않으려면
  1. 어떤 스레드가 즉시 할당할 수 없는 다른 자원 요청 -> 현재 점유중인 모든 자원이 선점됨
  2. 어떤 스레드가 자원 요청 -> 사용 가능하면 할당, 사용 불가능하면 추가 자원을 필요로 하는 다른 스레드에 할당되어 있는지 검사 -> 그렇다면 자원 선점
- ex) CPU 레지스터, DB 트랜잭션
- 일반적으로 mutex나 세마포에는 적용할 수 없음

#### 4) 순환 대기

- 모든 자원 유형에 순서를 부여, 그 순서대로 자원을 요청하도록 요구



## 6. 교착 상태 회피

- 교착 상태 예방 -> 장치 이용률 저하, 시스템 총처리율 감소
- 교착 상태를 회피하는 다른 대안: 자원이 어떻게 요청될지에 대한 추가 정보 요구

#### 1) 안전 상태

- 안전 순서: <T1, T2, T3, .... Tn>의 스레드 순서에서 T2는 현재 자원과 T1의 자원, T3는 현재 자원과 T1,T2의 자원, ... Tn은 현재 자원과 T1~Tn-1의 자원으로 수행 가능할 때 **안전**하다고 함
- 안전 상태면 교착 상태가 아님
- 불안전 상태면 교착 상태가 될 수 있음

#### 2) 자원 할당 그래프 알고리즘

- 자원 할당 그래프에서 **예약 간선** 추가
  - 예약 간선: 미래에 자원을 요청할 것이라는 의미
- 스레드가 자원을 요청할 때 예약 간선을 요청 간선으로 변환
  - 이 때 사이클을 형성하지 않아야 요청 허용

#### 3) 은행원 알고리즘

- 스레드가 가지고 있어야 할 자원의 최대 개수를 자원 종류마다 미리 신고해야함
  - 자원의 총 보유 수를 넘을 수 없음
- 스레드가 자원을 요청하고 허용되면 시스템이 안전 상태에 머무르는지 판단
  - 그렇지 않으면 다른 스레드가 끝날 때까지 대기



