# 함수형 인터페이스

- 추상메서드를 1개 가지는 인터페이스
```
interface FunctionalInterface{
	void someFunction();
}
```

- 람다는 함수형 인터페이스에만 사용할 수 있다.
```
FunctionalInterface f = new FunctionalInterface() {
    @Override
    public void someFunction() {
        System.out.println("Hello!");
    }
};
f.someFunction();
```
람다를 사용해서 위 코드를 아래처럼 간단하게 쓸 수 있다
```
FunctionalInterface f = () -> System.out.println("Hello!");
f.someFunction();
```

### Java8에서 제공하는 함수형 인터페이스 몇가지
- Runnable : 리턴 타입 (없음) / 매개변수 (없음)
```
Runnable r = () -> System.out.println("runnable");
```
- Supplier<T<T>> : 리턴 타입 (T) / 매개변수 (없음)
```
Supplier<String> s = () -> "Supply";
```

- Consumer<T<T>> : 리턴 타입 (없음) / 매개변수 (T)
```
Consumer<String> c = s -> System.out.println("param : " + s);
```
- Function<T,R> : 리턴 타입 (R) / 매개변수 (T)
```
Function<Integer, String> f = num -> "input is" + num;
```
- Predicate<T<T>> : 리턴 타입 (boolean) / 매개변수 (T)
```
Predicate<String> p = s -> s.length() < 10;
```
- UnaryOperator<T<T>> : 리턴 타입 (T) / 매개변수 (T)
```
UnaryOperator<String> u = s -> s + " is input";
```
- BinaryOperator<T<T>> : 리턴 타입 (T) / 매개변수 (T, T)
```
BinaryOperator<String> bo = (s, s2) -> s + " & " + s2;
```
- BiFunction<T,U,R> : 리턴 타입 (R) / 매개변수 (T, U)
```
BiFunction<String, String, Integer> bf = (s1, s2) -> s1.length() + s2.length();
```

### 참조
[Oracle docs](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html)