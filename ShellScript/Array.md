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

