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

> LPUSH [key] [value]
>
> RPUSH [key] [value]

- 리스트 처음/끝에 값 추가

