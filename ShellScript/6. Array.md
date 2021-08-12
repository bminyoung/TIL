# Array
## 1. 배열

> declare -a 변수명=(...)

- 각 배열 요소는 **공백**으로 구분
- 배열 요소는 인용부호로 감싸주는 것이 안전

```
$ declare -a array1=("water" "blue" "super")
$ declare -a array2=("melon" "mountain" "stars")

# "${!array1[@]}" : 인용부호를 써주어야함
$ for i in "${!array1[@]}"; do
>	printf "%s\t%s\t%s\n" "$i" "${array1[$i]}" "${array2[$i]}"
> done
0	water	melon
1	blue	mountain
2	super	starts
```



## 2. 배열과 glob, 루프

```
$ ARRAY=( "sky:blue" "snow:white" "night:black" "apple:red" )
$ for object in "${ARRAY[@]}"; do
>	KEY=${object%%:*}
>	VALUE=${object#*:}
>	printf "%s's color is %s.\n" "$KEY" "$VALUE"
> done
```

- object 에는 각 배열 요소가 들어감
- %%{문자열}* : 문자열 앞부분을 가져옴
- #*{문자열} : 문자열 뒷부분을 가져옴

---------

```
# 잘못된 예
$ files=$(ls)
$ files=($(ls))

# 바른 예
$ files=(*)
```



#### 실습

```
$ cat tech.txt
youtube,ai,alphago,arduino,IoT
$ ./makeTagDirectory.sh tech.txt
$ ll youtube.md ai.md alphago.md arduino.md IoT.md
$ cat ai.md
---
name: ai
title: 'ai'
---
```

- tech.txt 파일 내 ','로 구분된 문자열에 대해 각각 파일 생성하기

```
# makeTagDirectory.sh 파일

#!/usr/bin/env bash
IFS=$',' read -r -a array < $1
for elt in "${array[@]}"
do
	echo "---" > "$element.md"
	echo "name: $element" > "$element.md"
	echo "title: '$element'" > "$element.md"
	echo "---" > "$element.md"
done
```



## 3. find & -print0

```
# 정상 동작하지 않음
$ find . -name "*.mp3" | xargs rm -rf
```

- xargs : 파이프 기호 이전의 명령 수행 결과의 문자열을 그대로 rm 명령의 인수로 전달

- 파일 이름에 공백이 포함된 경우
  - 파일명="test file.mp3" => rm -rf test; rm -rf file.mp3 실행

```
# 마지막 널문자 확인
$ find . -iname "*.mp3" -print0 | hexdump -C

# -0 : 문자열을 널문자로 분리하려면 필수 옵션
$ find . -iname "*.mp3" -print0 | xargs -0 ls

$ find . -iname "*.mp3" -print0 | xargs -0 rm -rf
```

- -print0 : 모든 검색결과의 마지막에 널문자를 넣어줌



#### 추가) find

```
# -maxdepth 1 : 현재 경로에서만 검색 
$ find ./ -maxdepth 1 -iname '*.sh'

# -exec [명령...] \;
# {} : 검색 결과
$ find ./ -name "*.bak" -exec ls -l {} \;

# 홈 디렉토리에서 '.' 으로 시작하는 파일 검색
$ find ~/ -maxdepth 1 -name ".*"

# \(...\) : 2가지 이상 조건 조합
# 퍼미션이 644 & 소유권이 user인 파일
# -a : and
$ find ./ \( -user user -a -perm 644 \) -print | xargs ls -l
```

