

# Main Memory

## 1. Background
#### 1) 메모리 공간

- 프로세스는 각각의 메모리 공간을 가진다.
- 레지스터 = base 레지스터 + limit 레지스터
  - base 레지스터: 프로세스의 시작 위치를 저장
  - limit 레지스터: 프로세스에게 할당된 메모리의 크기
- 프로세스가 논리주소공간을 base 레지스터와 limit 레지스터로 지정
  - base 레지스터 <= 논리주소 공간 <= base 레지스터 + limit 레지스터

![logical_addr](./Image/Logical_addr.png)

- 다른 프로세스의 메모리에 접근하지 못하게 한다.

#### 2) 주소 바인딩

- 프로그램은 컴파일 후 메모리에 올라간다.
  - 컴파일러는 심볼릭 주소를 relocatable 주소로 바인딩
  - 링커(또는 로더)는 relocatable 주소를 절대 주소로 바인딩
- ![Addr-binding](./Image/Addr-binding.png)
- logical address: CPU에 의해 발생하는 메모리 주소
- physical address: 실제로 접근해야하는 메모리 주소

