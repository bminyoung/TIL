# Converting Object to Json (Redis)

- Redis로 캐시를 받아오는데 Date 타입을 필드로 가지는 객체를 Deserialize하는데 계속 실패했다

### 1. @DateTimeFormat
- 객체의 Date타입 필드에 DateTimeFormat 어노테이션을 추가해주었다
- 날짜 타입의 직렬화를 지원

```
@DateTimeFormat(pattern = "yyyy-MM-dd")
Date date;
```

### 2. GenericJackson2JsonRedisSerializer
- redisTemplate.setValueSerializer 의 매개변수로
new GenericJackson2JsonRedisSerializer(new ObjectMapper())을 넣어줌

```
//전
//redisTemplate.setValueSerializer(new GenericJackson2JsonRedisSerializer());
//후
redisTemplate.setValueSerializer(new GenericJackson2JsonRedisSerializer(new ObjectMapper()));
```

### 3. ObjectMapper
- 캐시를 받아올때 ObjectMapper를 사용

```
Object obj = redisTemplate.opsForValue().get(key);
url = mapper.convertValue(obj, MyClass.class);
```
