# Static / Non-static

### Non-static
- 인스턴스를 생성할 때 생성된다
- 각 인스턴스마다 하나씩 가지고 있다


### Static
- 코드 실행 시 생성된다 (JVM의 메서드 영역에 저장)
- 모든 인스턴스가 공유한다 (프로그램 전체에서 하나)
- static 함수 내에서 non-static 멤버나 함수를 사용하지 못한다 (non-static이 메모리에 있는지 없는지 모름)

```
class Test{
	//모든 Test 객체에서 공유
    static int a = 0;
}

Test t = new Test();
Test t2 = new Test();
t2.a = 10;
System.out.println(t.a); //10
```