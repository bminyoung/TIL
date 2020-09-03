# Builder Pattern
- 주로 객체를 생성할 때 이용한다.
- 생성자가 많은 경우 유용하다.
- Builder 패턴을 쓰지 않는 경우 -> 매개변수의 순서를 지켜야 함, 가독성이 좋지 않음
- 예시) Anrdroid의 alert

## Example
- 빌더 패턴을 쓰지 않은 코드
```
class User{
	private String id;
	private String password;
	private String name;
	private String gender;
	private String address;
	private Date joinDate;

	/* getter, setter */
}

...

public static void main(){
	String id = "testId";
	String pw = "testPw";
	String name = "nyoung";
	String gender = "female";
	String address = "testAdd";
	Date date = new Date();

	User user = new User();
	user.setId(id);
	user.setPassword(pw);
	user.setName(name);
	user.setGender(gender);
	user.setAddress(address);
	user.setJoinDate(date);

	//또는
	User user = new User(id, pw, name, gender, address, date);
}
```

- 빌더 패턴
```
class UserBuilder{
	private String id;
	private String password;
	private String name;
	private String gender;
	private String address;
	private Date joinDate;

	public UserBuilder id(String id){
		this.id = id;
		return this;
	}

	public UserBuilder password(String password){
		this.password = password;
		return this;
	}
	...

	public User build(){
		User user = new User();
		user.setId(id);
		user.setPassword(password);
		user.setName(name);
		user.setGender(gender);
		user.setAddress(address);
		user.setJoinDate(date);
		
		return user;
	}
}

...

public static void main(){
	UserBuilder builder = new UserBuilder();
	User user = builder
				.id("testId")
				.pw("testPw")
				...
				.build();
}
```
1. setter함수 => return 형식을 void -> Builder로 변경한다.
2. return this : Dot(.) Chain 방식을 쓸 수 있다.
3. builder() 함수로 객체를 반환한다.    


- 다음과 같은 builder 함수를 선언하면 builder객체를 만들지 않고 바로 사용할 수 있다.
```
public static UserBuilder builder(){
    return new UserBuilder();
}

...

public static void main(String[] args){
	User user = UserBuilder.Builder()
				.id("testId")
				.password("testPw")
				...
				.build();
```