# Shallow vs Deep

- 얕은 복제 : 주소값을 복사한다
- 깊은 복제 : 값 자체를 복사한다

```
//int, char 등의 primitive 타입은 값 자체를 대입
int a = 10;
b = a; // deep copy

//List 등의 타입은 주소값 대입
List<Integer> list1 = new ArrayList<>();
list1.add(1);
List<Integer> list2 = list1;
```


### Shallow copy
- 원본 / 복사본 -> 복사본을 변경하면 원본의 값도 변경됨
```
List<Integer> list1 = new ArrayList<>();
list1.add(1);
List<Integer> list2 = list1;
list2.add(2);
//list1, list2 모두 [1, 2] 값을 가지게 된다
```




### Deep copy
- 복사본을 변경해도 원본에는 영향x
- 사용자 정의 클래스에서는 clone 함수를 오버라이딩해서 재정의할 수 있다
```
List<User> copy = new ArrayList<>();
copy.addAll(copy); //addAll -> deep copy

```