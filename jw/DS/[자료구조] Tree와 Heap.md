##### 최지우 작성
<img width="437" alt="스크린샷 2021-02-09 오후 8 08 16" src="https://user-images.githubusercontent.com/29567741/107355241-8d59fb80-6b12-11eb-9601-a301e72adfb7.png">

## 트리(Tree)
- 비선형 구조 ⇒ 1:n 관계를 가지는 자료구조
- 다:다 ⇒ 그래프, 1:다 + 계층 ⇒ 트리
- 상위 입장에서는 하위가 여러개이지만, 하위 입장에서는 상대가 하나면 트리를 쓸 수 있다. 한 개의 루트 노드만이 존재하며 모든 자식 노드는 한개의 부모 노드만을 가진다.
- 리스트에서 head를 가지고 있으면 리스트 전체를 가지고 있는 것과 같음. 트리에서는 노드가 그 역할을 한다.
- 노드가 n개인 트리는 항상 n-1개의 간선(edge)를 가진다.

### 용어
<img width="790" alt="스크린샷 2021-03-02 오후 8 37 53" src="https://user-images.githubusercontent.com/29567741/109643142-2b336a00-7b97-11eb-9d2b-5c0a13b082b9.png">
- 루트 노드(root node) : A
부모가 없는 노드, 트리는 단 하나의 루트 노드만을 가진다.
- 단말 노드(leaf node) : F, G, H, I, J
차수가 0인 노드, 즉 자식 노드가 없는 노드
- 형제 노드(sibling node) : H와 I는 형제 노드이다.
같은 부모 노드의 자식 노드들
- 조상 노드 : H의 조상노드는 D, B, A이다.
간선을 따라 루트 노드까지 이르는 경로에 있는 모든 노드들
- 자손 노드 : B의 자손 노드들은 D, E, H, I, J이다.
서브 트리에 있는 하위 레벨의 노드들
- 간선(edge) : 노드를 연결하는 선
- 서브 트리 : 부모 노드와 연결된 간선을 끊었을 때 생성되는 트리
- 차수(degree)
-- 노드의 차수 : 노드에 연결된 자식 노드의 수(간선 수)
-- 트리의 차수 : 트리에 있는 노드의 차수 중에서 가장 큰 값
- 높이
-- 노드의 높이 : 루트에서 노드에 이르는 간선의 수, 즉 노드의 레벨
-- 트리의 높이 : 트리에 있는 노드의 높이 중에서 가장 큰 값, 즐 최대 레벨


### 종류
#### 이진트리(Binary Tree)
<img width="304" alt="스크린샷 2021-03-02 오후 8 38 04" src="https://user-images.githubusercontent.com/29567741/109643165-32f30e80-7b97-11eb-9a23-92872a173f78.png">
모든 노드들이 2개의 서브트리를 갖는 특별한 형태의 트리이다. 각 노드가 자식노드를 최대한 2개까지만 가질 수 있다.

#### 이진 탐색 트리(Binary Search Tree)
<img width="317" alt="스크린샷 2021-03-02 오후 8 38 15" src="https://user-images.githubusercontent.com/29567741/109643176-37b7c280-7b97-11eb-87b1-ab11b7a326d9.png">
모든 부모 노드들의 left child는 부모 노드의 데이터보다 값이 작아야 하고, right child는 부모 노드의 값보다 커야한다. 여기서 중위순회(Inorder Travel)을 적용하면 오름차순 정렬이 된다.

#### 정 이진 트리(Full Binary Tree)
<img width="332" alt="스크린샷 2021-03-02 오후 8 38 21" src="https://user-images.githubusercontent.com/29567741/109643197-3be3e000-7b97-11eb-8f9d-bb09dcbe9384.png">
자식 노드가 아예 없거나, 최대 둘뿐인 tree. 자식을 하나만 가진 노드가 없어야 한다. 포화 이진 트리의 하위 종류이다.

#### 포화 이진 트리(Perfect Binary Tree)
<img width="354" alt="스크린샷 2021-03-02 오후 8 38 29" src="https://user-images.githubusercontent.com/29567741/109643211-40a89400-7b97-11eb-8434-1386abcd76f7.png">
모든 노드가 0개 혹은 2개의 자식노드를 가지며 모든 리프노드가 똑같은 레벨에 있다. 완벽한 피라미드 모양.

#### 완전 이진 트리(Complete Binary Tree)
<img width="648" alt="스크린샷 2021-03-02 오후 8 38 38" src="https://user-images.githubusercontent.com/29567741/109643236-456d4800-7b97-11eb-9a49-4ccfb18651fc.png">
마지막 레빌을 제외한 모든 레벨에 노드가 채워져 있으며 , 마지막 레벨은 왼쪽부터 채워져 있어야한다. 마지막 레벨은 꽉 차있을 필요는 없다.

#### 편향 이진 트리(Skewed Binary Tree)
<img width="231" alt="스크린샷 2021-03-02 오후 8 38 45" src="https://user-images.githubusercontent.com/29567741/109643245-49996580-7b97-11eb-81ae-cfd1e872bd46.png">
말 그대로 노드들이 전부 한 방향으로 편향된 트리이다.


---

## 힙(Heap)
완전 이진 트리의 일종, 우선순위 큐를 위해 만들어진 자료구조이다.
힙을 이용하여 우선순위 큐를 구현하면 데이터를 삽입, 삭제하는데 longn의 시간이 걸린다. 여러 개의 갑들 중에서 최댓값이나 최솟값을 빠르게 찾아낼 수 있는 자료구조이다.

### 종류
- 최대 힙(max heap)
부모 노드의 키값 >= 자식노드의 키값
- 최소 힙(min heap)
부모 노드의 키값 <= 자식노드의 키값
<img width="770" alt="스크린샷 2021-03-02 오후 8 38 55" src="https://user-images.githubusercontent.com/29567741/109643264-5027dd00-7b97-11eb-916c-d711c6e2f54c.png">

### 특징
- 최대값과 최소값을 O(1)의 속도로 구할 수 있다.
- 보통 **배열**을 이용하여 구현한다.
- 구현을 쉽게 하기 위해서 인덱스 1부터 시작한다.
- 인덱스
-- 왼쪽 자식의 인덱스 : (부모의 인덱스) * 2
-- 오른쪽 자식의 인덱스 : (부모의 인덱스) * 2 + 1
-- 부모의 인덱스 : (자식의 인덱스) / 2
<img width="718" alt="스크린샷 2021-03-02 오후 8 39 07" src="https://user-images.githubusercontent.com/29567741/109643281-56b65480-7b97-11eb-82ec-2dbff4e7991c.png">

### 데이터 삽입
#### max heap일 경우
1. 데이터를 일단 맨 마지막 인덱스에 추가한다.
2. 부모 노드와 비교하여 부모 노드보다 작다면 그대로 두고
3. 부모 노드보다 크다면, 부모 노드와 위치를 바꿔준다.

![1](https://user-images.githubusercontent.com/29567741/109643330-6df54200-7b97-11eb-9372-72b6dffe9784.png)


### 데이터 삭제
#### max heap일 경우
1. root 노드를 삭제한다.
2. root 노드의 자리에 맨 마지막 노드를 가져온다.
3. heap을 재구성한다. (만약 자식 노드보다 크다면 그대로 두고, 작다면 자식노드와 값을 바꾼다.

![2](https://user-images.githubusercontent.com/29567741/109643342-72b9f600-7b97-11eb-9105-dc9c72fcfb73.png)


<br>
<br>
<details>
<summary>출처</summary>
https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html
https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html
https://it-and-life.tistory.com/164
https://sexycoder.tistory.com/81
http://www.secmem.org/blog/2019/05/09/%ED%8A%B8%EB%A6%AC%EC%9D%98-%EC%A2%85%EB%A5%98%EC%99%80-%EC%9D%B4%ED%95%B4/
</details>
