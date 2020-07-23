# 박싱 / 언박싱

## 1. Wrapper 클래스
- primitive (int, char, float 등) 형은 컬렉션과 같은 클래스를 이용하지 못한다
	(ex- List<int<int>> 는 사용할 수 없다)
- 이를 사용하기 위해 사용하는 것이 Wrapper 클래스
- Integer, Character, Float 등

### 2. 박싱
- primitive -> wrapper
```
int number = 100;
Integer integer1 = new Integer(number); //명시적 변환
Integer integer2 = number; //묵시적 변환
```


### 3. 언박싱
- wrapper -> primitive
```
int number = 100;
Integer num = new Integer(number);
int unbox = num.intValue(); //명시적 변환
int unbox = num; //묵시적 변환
```