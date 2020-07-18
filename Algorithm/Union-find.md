# Union-find
- disjoint-set, grouping 문제에 쓸 수 있다
- 원소가 같은 집합에 속해있는지 확인
- 이 문서에서 root = 집합의 대표 번호, 작은 숫자로 맞춘다
- 사용하는 함수
1. Initialize : 각 원소의 root를 자기자신으로 설정
2. Union : 두 집합을 하나로 합침 (같은 root를 갖게 한다)
3. Find : 원소의 root 번호를 검색한다


```
// 1.Initialize
for (int i = 1; i <= root.length; i++) { // initialize
    root[i] = i;
}
```

```
// 2. Union
void union(int[] root, int a, int b){
    int root1 = findRoot(root, a);
    int root2 = findRoot(root, b);
    if(root1 < root2) root[root2] = root1;
    else if(root1 > root2) root[root1] = root2;
}
```

```
// 3. Find
// line 3 : 경로 압축 과정 (root값을 갱신해준다)
1 void findRoot(int[] root, int element){
2     if(root[element] == element) return element;
3     return root[element] = findRoot(root, root[element]);
4 }

```


![unionFind](./img/Union-find.png)
1) Initialize    

|node|1|2|3|4|5|6|
|---|---|---|---|---|---|---|
|root|1|2|3|4|5|6|

2) 5-6 연결    

|node|1|2|3|4|5|6|
|---|---|---|---|---|---|---|
|root|1|2|3|4|5|**5**|

3) 3-5 연결    

|node|1|2|3|4|5|6|
|---|---|---|---|---|---|---|
|root|1|2|3|4|**3**|5|

4) 2-5 연결    

|node|1|2|3|4|5|6|
|---|---|---|---|---|---|---|
|root|1|2|**2**|4|**2**|5|
- find 함수의 line 3에 의해 node 3, 5의 값 모두 변경된다

5) 4-6 연결    

|node|1|2|3|4|5|6|
|---|---|---|---|---|---|---|
|root|1|2|2|**2**|2|**2**|
- 4의 root(=4) 와 6의 root(=2, 6->5->2) 를 비교해서 작은 값인 2를 root로 한다

##### 관련문제
- BOJ 1717, 1976, 4195, 10775
