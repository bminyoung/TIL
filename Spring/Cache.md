# 캐시

### 1. pom.xml
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

### 2. application.properties
```
spring.cache.type=redis
spring.redis.host=localhost
spring.redis.port=6379
```

### 3. @EnableCaching 추가
```
@EnableCaching
@SpringBootApplication
public class ExampleApplication {
	public static void main(String[] args) {
		SpringApplication.run(UrlShorteningApplication.class, args);
	}
}
```

### 4. 캐시 사용
- key-value
#### 4-1. 캐시 등록
- @Cacheable : 있으면 가져오기, 없으면 저장
- @CachePut : 캐시 저장
```
//key를 지정하지 않으면 파라미터를 key로 지정한다
@Cacheable(value = "userName", key="#name")
public String find(String name) {
	...
    return name;
}
```

#### 4-2. 캐시 삭제
- @CacheEvict
```
@CacheEvice(value = "userName", key="#name")
public void delete(String name) {
	...
}
```


참고
[Spring](https://docs.spring.io/spring/docs/current/spring-framework-reference/integration.html#cache)