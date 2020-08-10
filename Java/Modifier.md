# Modifier

### 1. static
- 인스턴스를 생성하지 않고 사용가능

### 2. final
- 값, 내용을 변경할 수 없음

### 3. abstract
- 추상클래스, 추상메서드에 사용

### 4. 접근제어자
- 캡슐화를 하는데 사용한다
- class에는 public, default만 사용가능
- 접근제어자를 명시하지 않으면 default    

|---|public|protected|default|private|
|---|---|---|---|---|
|같은클래스|o|o|o|o|
|같은패키지|o|o|o|x|
|다른패키지,상속관계|o|o|x|x|
|그 외|o|x|x|x|
