# Git Command (CLI)

### 1. 저장소 만들기
- 원하는 폴더로 이동하고 실행
#### 1-1 새 저장소 만들기
`$ git init`

#### 1-2 원격저장소 복사
`$ git clone [저장소 주소]`
>(Example) 
>$ git clone https://github.com/bminyoung/TIL.git

### 2. Add
`$ git add [파일 이름]` 또는 `$ git add .` 또는 `$ git add *`

- 변경된 파일들을 인덱스(staging area)에 올린다
- 두번째, 세번째는 모든 파일 add

### 3. Commit
`$ git commit -m "메시지"`

- 로컬 저장소에 반영되었지만 원격 저장소에는 반영이 안됐다 (=> 4. Push)
- 메시지는 생략가능하나 써주는 습관을 들이자

※ `$ git commit -am "메시지"` : add와 commit 을 한꺼번에 처리

### 4. Push
#### 4-1. Push 전에
> 원격 저장소를 복제한 게 아니라면? (1-1 git init)
> -> 저장소를 연결해주어야 한다!

` $ git remote add origin [저장소 주소]`

- origin : 원격 저장소 이름, 다른 이름이어도 됨
		저장소를 clone했다면 원격 저장소 이름은 origin으로 자동 지정

> 협업 중이라면?
>  -> 코드를 가져와서 병합 후 push 해야한다

`$ git pull`

#### 4-2. Push
`$ git push origin master`

- master : 기본 브랜치, master 대신 push 하고싶은 브랜치 이름을 넣으면 됨

※ `$ git push -u origin master`
- origin 이라는 원격저장소와 master라는 브랜치를 연결, 이후 `$ git push` 로 간단하게 쓸 수 있다
