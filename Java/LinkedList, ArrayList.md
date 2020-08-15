﻿# LinkedList / ArrayList

### LinkedList
- 노드의 주소값들이 연결되어있는 형태
- 각 노드의 전후 노드 정보(주소)만 알면 된다.

- 추가
	1. 해당 데이터의 정보를 담은 노드(A)를 생성한다.
	2. 추가할 데이터의 이전 인덱스 노드(B)를 A로 연결한다.
	3. A의 다음 노드를 원래 B의 다음 노드였던 노드(C)로 설정한다.
- 삭제
 	0. 삭제할 노드(A)의 이전 노드(B)와 다음 노드(C)
	1. B 노드의 다음 노드를 C 노드로 설정한다.
	2. A 노드를 삭제한다.
- 검색



### ArrayList
- 배열과 비슷한 형태 (데이터가 연속적으로 연결)

- 추가
	1. (ArrayList의 크기 + 1) 만큼의 ArrayList를 새로 할당한다.
	2. 추가할 인덱스를 기준으로 데이터를 적절한 위치로 복사한다.
	3. 인덱스 자리에 데이터를 추가한다.