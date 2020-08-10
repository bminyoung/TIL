# String vs StringBuffer vs StringBuilder


### String
- 불변한다는 속성을 갖고 있다
- 추가, 삭제 등 연산이 적고 참조가 많은 경우 사용하는 것이 좋다
```
String str = "hello";
str += " world";
System.out.println(str); //hello world
```
- 실제로 [hello], [hello world] 두 객체가 존재한다.
- "hello world" 객체를 새로 만들고 이를 참조하게 된다
- "hello" 객체는 나중에 GC에 의해 제거된다

### StringBuilder, StringBuffer
- 가변적인 속성을 갖고 있다
- 연산이 많은 경우 사용하는 것이 좋다
```
StringBuilder sb = new StringBuilder("hello");
sb.append(" world");
System.out.println(sb.toString()); //hello world
```
- 연산할 때 새로운 객체를 만들지 않고 원본을 수정한다

- 차이점 : 동기화 지원 여부

|StringBuilder|StringBuffer|
|---|---|
|동기화 지원 x|동기화 지원 o|
|멀티쓰레드 x|멀티쓰레드 o<br>(thread-safe)|

- 싱글쓰레드 환경에서 연산이 많으면 StringBuilder를 쓰자