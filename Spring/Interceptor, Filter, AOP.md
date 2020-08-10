# Interceptor / Filter / AOP



### Interceptor
- Spring 영역에서 컨트롤러에 관한 요청을 인터셉트해서 처리한다.
- Spring의 Bean객체에 접근할 수 있다.
- 로그인 체크, 권한 체크 등
- preHandler / postHandler / afterCompletion
	- preHandler : 컨트롤러에 도달하기 전
	- postHandler : 컨트롤러 도달 후 view를 호출하기 전
	- afterCompletion : view를 호출한 후

### Filter
- Spring 영역 밖에서 필터링을 처리한다.
- 한글 처리 등
- init / doFilter / destroy 함수
	- init : 필터 인스턴스를 초기화 (서비스 실행 시)
	- doFilter : 필터할 내용
	- destroy : 필터 인스턴스 destroy



### [AOP](./AOP.md)
> 관점(Aspect) 지향 프로그래밍

- OOP를 보완하기 위해 나왔다.
- 프로그래밍 시 관점을 바꾸어 종단면을 본다. (실행 전후 등 공통 부분)
- 로깅,  에러 처리 등
- @Before, @After, @AfterReturning, @AfterThrowing, @Around
	- @Before : 메서드 실행 **전**
	- @After : 메서드 실행 **후**
	- @AfterReturning : 메서드의 **정상적인 실행** 후
	- @AfterThrowing : 메서드 실행 중 **예외 발생**했을 때
	- @Around : 메서드 실행 **전후**