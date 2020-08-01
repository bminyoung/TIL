﻿# 마크다운

## 1. 헤더
- 글머리 (1~6)
```
# h1
## h2
### h3
#### h4
##### h5
###### h6
```
# h1
## h2
### h3
#### h4
##### h5
###### h6
####### h7

## 2. 목록
#### 2-1. 순서있는 목록
- 숫자 + .
```
1. 1번
2. 2번
3. 3번
```
1. 1번
2. 2번
3. 3번

#### 2-2. 순서없는 목록
- -, *, + (섞여도 된다)
```
- 1번
+ 2번
* 3번
- 4번
```
- 1번
+ 2번
* 3번
- 4번

## 3. 텍스트박스
#### 3-1. 텍스트 한줄
- ` 기호
```
`이곳에 입력`
```
`이곳에 입력`

#### 3-2. 텍스트 블록
- > 기호 (여러번 들여쓰기 가능)
```
> 이곳에 입력
> > 이곳에 입력
```
> 이곳에 입력
> > 이곳에 입력

#### 3-3. 코드 블록
- ` 기호 3개
- 뒤에 언어를 쓰면 하이라이팅 기능
<pre>
<code>
```java
System.out.println("Example");
```
</code>
</pre>

```java
System.out.println("Example");
```

## 4. 링크
- \[텍스트](링크)
- 링크에 띄어쓰기가 있는 경우 %20으로 대체
```
[Git](https://github.com/)
```
[Git](https://github.com/)



## 5. 이미지
- ![텍스트](이미지 링크)
```
![image](./image.jpg)
```
![Image](./image.jpg)

## 6. 표
```
|제목1|제목2|제목3|
|---|---|---|
|내용1|내용2|내용3|
```
|제목1|제목2|제목3|
|---|---|---|
|내용1|내용2|내용3|


## 기타
- 특수문자 앞에 \를 입력하면 그대로 쓸 수 있다
```
\[제목]
```
\[제목]

- <> 기호 이용
```
<text<text>>
```
<text<text>>