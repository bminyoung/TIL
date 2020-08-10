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
- Spring 영역 밖에서 필터링을 처리한다
- 한글 처리 등
- init / doFilter / destroy 함수
	- init : 필터 인스턴스를 초기화한다 (서비스 실행 시)
	- doFilter : 필터할 내용
	- destroy : 필터 인스턴스 destroy


### AOP