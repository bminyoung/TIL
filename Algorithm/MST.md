# MST (Minimum Spanning Tree)


### 1. Spanning Tree
- 모든 정점이 연결된 그래프
- 사이클 x
- 포함하는 간선 갯수는 (정점갯수 - 1) 개

### 2. Minumum Spanning Tree
- 간선의 가중치 총합이 최소가 되는 Spanning Tree

### 3. MST 알고리즘
- [Kruskal 알고리즘](./Kruskal.md)
- [Prim 알고리즘](./Prim.md)

### 4. 시간복잡도
- Kruskal
	- 간선 정렬 + Union-find = 간선 정렬 시간복잡도 = O(ElogE)
	- 간선이 적은 경우 좋다
- Prim
	- 배열을 이용해서 최소 간선을 찾는 경우 : O(V^2)
	- 최소힙을 이용해서 최소 간선을 찾는 경우 : O(ElogV)
	- 정점이 적은 경우 좋다

##### 관련문제
- BOJ 9372, 1197, 4386, 1774, 2887
