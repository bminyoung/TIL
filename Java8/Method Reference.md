# 메서드 레퍼런스

- 람다식을 더 간단하게 표현할 수 있다
- 생략할 수 있는 것들은 더 생략한다


### 1. Static 메서드 레퍼런스
- [클래스명::정적메서드] 형식

```
Function<String, Integer> f = s -> Integer.parseInt(s);
```
- 위의 식을 아래처럼 쓸 수 있다
- 매개변수가 String 값, 리턴값이 int값이라는 것을 알 수 있다
```
Function<String, Integer> f = Integer::parseInt;
```

### 2. Constructor 메서드 레퍼런스
- [클래스명::new] 형식
```
class Person{
    String name;
    public Person(String name) {
        this.name = name;
    }
}
```

```
Function<String, Person> f = s -> new Person(s);
```
- 위의 식을 아래처럼 쓸 수 있다
- 생성자에 필요한 매개변수(String 값)가 명확하다
```
Function<String, Person> f = Person::new;
```

### 3. Instance 메서드 레퍼런스
```
class Intro{
    public String introduction(String name){
	    return "name is " + name;
	}
}
```
3-1. 특정 객체의 인스턴스 메서드
- [객체명::인스턴스메서드] 형식
- 람다식 밖의 변수에 접근한다
```
String str = "Hello";
Supplier<Integer> len = () -> str.length();
```
- 위의 식을 아래처럼 쓸 수 있다
```
String str = "Hello";
Supplier<Integer> len = str::length;
```

3-2. 특정 타입의 임의의 객체의 인스턴스 메서드
- [클래스명::인스턴스메서드] 형식
- 람다식 내부의 변수에 접근한다
```
Function<String, Integer> f = s -> s.length();
```
- 위의 식을 아래처럼 쓸 수 있다
```
Function<String, Integer> f = String::length;
```

### 참조
[Oracle docs](https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html)
