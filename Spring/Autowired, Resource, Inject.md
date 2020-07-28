# Autowired, Resource, Inject

```
@Configuration
public class Config {
	@Bean
	public UserA user() {return new UserA();}
	
	@Bean
	public UserA user2() {return new UserA();}
	
	@Bean
	public UserB userB() {return new UserB();}
}
```

### 1. Resource
- **이름**으로 DI 객체 선택
- Java에서 지원
- name 속성
```
@Resource
private UserA user; //첫번째 Bean 주입
```
- 다음과 같으면 오류
```
@Resource
private UserA aaa; // 어떤걸 주입해야할지 모름

@Resource
private UserA userB; //UserB 객체를 주입 -> 타입 캐스팅 오류
```

- 타입 캐스팅 오류의 경우, 강제로 연결을 해줄 수 있다(name)
```
@Resource(name="user2")
private UserA userB;
```


### 2. Autowired
- **타입**으로 DI 객체 선택
- Spring에서 지원
- @Qualifier
```
// UserA 타입 객체 자동주입
@Autowired
private UserA aaa;
```
- 다음과 같으면 오류
```
@Autowired
UserA aaa; // 어떤걸 주입해야할지 모름
```
- 강제 연결을 해줄 수 있다 (@Qualifier)
```
@Autowired
@Qualifier("user2")
private User aaa;
```

### 3. Inject
- **타입**으로 DI 객체 선택
- Java에서 지원
- @Autowired와 비슷
```
@Inject
private UserA aaa;
```
