# Redis command

#### Set

> SET [key] [value]
>
> SET [key] [value] EX [timeout]



#### Get

> GET [key]
>
> \> [value]



#### EXISTS

> EXISTS [key]
>
> \>1 (if key exists)
>
> \>0 (else)



#### INCR, DECR

> INCR [key]
>
> DECR [key]

- key값을 1 증가/감소시킴

- atomic 연산



#### INCRBY, DECRBY

> INCRBY [key] [value]
>
> DECRBY [key] [value]

- key값을 value만큼 증가/감소시킴



#### DEL

> DEL [key]



#### EXPIRE

> EXPIRE [key] [timeout]

- timeout 만큼의 시간이 지난 뒤 key 삭제



#### TTL

> TTL [key]
>
> \> [seconds]
>
> \> -1 (key가 삭제될 예정 없음)
>
> \> -2 (key가 존재하지 않음)

- key 삭제까지 남은 시간



#### PERSIST

> PERSIST [key]

- expire 취소



### *리스트*

#### LPUSH, RPUSH

> LPUSH [key] [value1] [value2] [value3] ...
>
> RPUSH [key] [value1] [value2] [value3] ...

- 리스트 처음/끝에 값 추가



#### LPOP, RPOP

> LPOP [key]
>
> RPOP [key]
>
> \> [value]

- 리스트 처음/끝에서 값 가져오기



#### LRANGE

> LRANGE [key] [start] [end]

- 리스트(key) subset 가져오기



### *Set*

#### SADD

> SADD [key] [value1] [value2] ...
>
> \> 0 (값이 이미 있음)
>
> \> 1 (추가됨)

- set에 값 추가



#### SREM

> SREM [key] [value]

- set에서 값 제거



#### SMEMBERS

> SMEMBERS [key]

- set 값 가져오기



#### SISMEMBER

> SISMEMBER [key] [value]

- 값이 set에 포함되었는지



#### SUNION

> SUNION [set1] [set2]

- set 합치기



#### SPOP

> SPOP [key] [n]
>
> \> [value_1] [value_2] ... [value_n]

- set에서 n개 꺼내기



#### ZADD

> ZADD [key] [score] [value]

- set에 값 추가
- score 기준으로 정렬



### *Hash*

#### HSET, HMSET

> HSET [key] [field] [value]
>
> HMSET [key] [field1] [value1] [field2] [value2] ...

- hash에 값 추가



#### HGET

> HGET [key] [field]
>
> \> [value]

- hash에서 해당 필드 값 가져오기



#### HGETALL

> HGETALL [key]
>
> \> 1) [value1]
>
> 2) [value2]
>
> ....
>
> n) [value_n]

- hash에서 모든 필드 값 가져오기



#### HINCRBY

> HINCRBY [key] [field] [num]
>

- 해당 필드 값 1 증가



#### HDEL

> HGET [key] [field]
>

- hash에서 해당 필드 값 삭제