# 람다 표현식

- 익명 함수를 만들기 위한 식
- 함수 지향적 프로그래밍
- [함수형 인터페이스](./Functional%20Interface.md)에만 쓸 수 있다
- 형식 : (매개변수) -> {함수 내용}

- 코드 수를 줄일 수 있다.
```
MyInterface mi = new MyInterface() { //1
    @Override
    public void someFunction(String str) { // 2
        System.out.println(str);
    }
};
mi.someFunction("Hello!");
```
1 : MyInterface 라는 타입을 이미 명시    
2 : 오버라이드해야할 함수가 1개뿐
```
MyInterface mi = (String str){
    System.out.println(str);
};
mi.someFunction("Hello!");
```
함수가 1개뿐이라서 매개변수 타입도 알 수 있음,
함수 내용이 한줄이라면 중괄호도 생략가능
매개변수가 한개라면 소괄호도 생략가능
```
MyInterface mi = str -> System.out.println(str);
mi.someFunction("Hello!");
```
