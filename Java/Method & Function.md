# Method / Function

### Method(메서드)
- 클래스에 종속되어 있다
- 해당 객체가 생성되어 있어야 사용이 가능하다(static 제외)
- 입력값이 같아도 출력값이 다를 수도 있다

### Function(함수)
- 입력값이 같으면 출력값이 항상 같다

```
class User{
	String name;
	...
	String like(String thing){
		return name + " like " + thing;
	}
	...
}
User user = new User("AAA");
String like = user.like("apple"); //AAA like apple
user.setName("BBB");
like = user.like("apple"); //BBB like apple
```

```
//name에 같은 값이 들어가면 리턴값도 같다
String getName(String name){
	return "name is " + name;
}
String name = getName("AAA"); //name is AAA
name = getName("AAA"); //name is AAA
```
