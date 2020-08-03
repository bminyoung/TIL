# Mutable / Immutable

### Mutable
- 객체 생성 후에도 변경할 수 있다

### Immutable
- 객체가 생성되면 변경할 수 없다
- Integer 등의 Wrapper 클래스, String
- 멀티쓰레드 환경에서 안전하다 (값 변경이 안되기 때문)
- 변경하려고 하면 새로운 객체를 생성해서 반환한다 (-> GC에 부담)


### String
- String은 immutable, StringBuilder와 StringBuffer는 mutable
[String vs StringBuilder vs StringBuffer](./String%20vs%20StringBuilder%20vs%20StringBuffer.md)