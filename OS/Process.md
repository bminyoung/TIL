# Process
## 1. Process Concept
> 실행중인 프로그램
>
> 작업의 단위

- 작업을 수행하기 위해 특정 자원이 필요하다
  - CPU time, 메모리, 파일, I/O device

#### 1) 메모리 영역

- Text 영역: 실행가능한 코드
- Data 영역: 전역 변수
- Heap 영역: 프로그램 실행 중 **동적으로 할당되는 메모리**
- Stack 영역: 함수 파라미터, 지역 변수 등 일시적인 데이터 저장공간



#### 2) 프로세스 상태

- New: 프로세스가 생성됨
- Running: cpu를 점유해서 프로세스의 명령 실행

- Waiting: 이벤트 발생을 대기
- Ready:  cpu 점유할 준비가 된 상태
- Terminated: 프로세스가 종료됨



#### 3) 프로세스 관리

- TCB(Task Control Block)

- PCB (Process Control BLock)
  - 프로세스 상태
  - 프로그램 카운터
  - CPU 레지스터
  - CPU 스케줄링 정보
  - 메모리 관리 정보
  - 계정 정보
  - I/O 상태 정보