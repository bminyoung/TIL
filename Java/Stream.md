# 스트림

- 기존 컬렉션은 삽입, 제거 연산 위주
- 스트림은 컬렉션이나 배열의 각 원소에 대한 반복 작업이 가능하다
- 코드를 줄이고 가독성을 높일 수 있다
- 생성 -> 중간 연산 -> 최종 연산
- 최종 연산을 실행할 때 중간 내용도 실행된다 (미리 실행하지 않음)
- 메서드 체이닝 형식


### 1. 생성
- 배열
```
String[] strArr = new String[]{"AAA", "BBB", "CCC"};
Stream<String> stream = Arrays.stream(strArr);
```

- 컬렉션
```
List<String> list = Arrays.asList("AAA", "BBB", "CCC");
Stream<String> stream = list.stream();
```

- 직접 생성
```
Stream<String> stream = Stream.of("AAA", "BBB", "CCC");

// 1~30을 원소로 가지는 스트림 생성
// 무한히 생성하므로 limit을 명시해주어야 한다
Stream<Integer> nums = Stream.iterate(1, n -> n+1).limit(30);
```


### 2. 중간 연산

- filter : 조건에 맞는 원소만 뽑는다
```
Stream<Integer> nums = Stream.iterate(1, n -> n+1).limit(30);
nums.filter(n -> n % 2 == 0);
```
- map : 각 원소에 함수를 적용한다
```
//1~30 -> 2~31
nums.map(n -> n+1);
```
- peek : 각 원소에 적용하는 것은 map이랑 같지만 인자로 Consumer를 넣는다
```
nums.peek(n -> System.out.println(n));
```

- 중간 연산 결과는 stream으로, 메서드 체이닝을 이용할 수 있다
```
nums.filter(n -> n % 2 == 0)
    .map(n -> n+1)
    .peek(n -> System.out.println(n));
```
위의 코드만으로는 실행되지 않는다 (최종 연산 시 실행)
따라서 출력도 되지 않는다


### 3. 최종 연산

- count : 스트림 원소 갯수를 반환한다
```
Stream<Integer> nums = Stream.iterate(1, n -> n+1).limit(30);
long cnt = nums.count();
```
- reduce : 함수를 실행하여 하나의 결과를 만든다
```
int sum = nums.reduce((a, b) -> a+b).get();
```
- collect : 스트림을 컬렉션 등의 자료형으로 변환한다
```
List<Integer> list = nums.collect(Collectors.toList());
```
- match : 조건을 만족하는지 true/false값을 반환한다 (anyMatch, allMatch, noneMatch)
```
boolean b = nums.allMatch(n -> n < 100);
```
- foreach : 스트림의 원소 각각에 대해 실행한다 (peek:중간연산, foreach:최종연산)
```
nums.forEach(n -> System.out.println(n));
```



### 참조
[더 많은 함수보기_Oracle docs](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/stream/Stream.html)

