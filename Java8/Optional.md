# 옵셔널 (Optional)

- NullPointerException 을 방지하기 위한  클래스


### 1. 생성
- Optional.of : null값을 받으면 예외가 발생한다
```
String str = "Hello";
Optional<String> op = Optional.of(str);
```

- Optional.empty : 빈 객체를 생성한다
```
Optional<String> op = Optional.empty();
```

- Optional.ofNullable : null값일 수도 있다
```
String str = "Hello";
Optional<String> op = Optional.ofNullable(str);
```


### 2. API

- orElse : 값을 반환한다. null값이면 인자를 반환한다.
```
String str = null;
Optional<String> op = Optional.ofNullable(str);
str = op.orElse("str is null");
```

- orElseGet : 값을 반환한다. null값이면 supplier의 반환값을 그대로 반환한다.
```
String str = null;
Optional<String> op = Optional.ofNullable(str);
str = op.orElseGet(() -> "str is null");
```

- orElseThrow : 값을 반환한다. null값이면 supplier의 예외 반환값을 그대로 반환한다.
```
String str = null;
Optional<String> op = Optional.ofNullable(str);
str = op.orElseThrow(() -> new NullPointerException());
```

- isPresent : null값 여부를 반환한다.
if문과 사용하면 일반적인 널 체크(==null)와 같은 기능이다
```
String str = null;
Optional<String> op = Optional.ofNullable(str);
boolean isNull = op.isPresent();
```

- ifPresent : null값이 아니면 메서드를 실행한다.
```
String str = null;
Optional<String> op = Optional.ofNullable(str);
op.ifPresent(s -> System.out.println(s));
```

- get : 값을 반환한다. null값이면 NoSuchElementException을 발생시킨다.
```
String str = null;
Optional<String> op = Optional.ofNullable(str);
str = op.get();
```

- filter : null값이 아니고 조건을 만족하면 값을 반환한다.
```
String str = "Hello optional";
Optional<String> op = Optional.ofNullable(str);
op.filter(s -> s.contains("op"));
```


### 3. Example
```
1 Object obj = getObject();
2 if(obj != null){
3     Object2 obj2 = obj.getObject2();
4     if(obj2 != null){
5         obj = obj2.getObject();
6     }
7 }
```

```
Optional.ofNullable(getObject()) //line1
        .map(Object::getObject2) //line3
        .map(Object2::getObject) //line5
        .orelse(new Object())
```




### 참조
[Oracle docs](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html)

