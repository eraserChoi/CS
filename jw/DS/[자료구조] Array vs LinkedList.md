##### 최지우 작성
<img width="437" alt="스크린샷 2021-02-09 오후 8 08 16" src="https://user-images.githubusercontent.com/29567741/107355241-8d59fb80-6b12-11eb-9601-a301e72adfb7.png">

## Array와 LinkedList의 차이가 무엇인가요?(N사 전화면접)
### 1. 접근
- Array : Random Access를 지원한다. 요소들을 인덱스를 통해 직접 접근할 수 있다. 따라서 특정 요소에 접근하는 시간복잡도는 O(1)이다.
- Linkedlist는 Sequential Access를 지원한다. 어떤 요소를 접근할 때 순차적으로 검색하며 찾아야 한다. 따라서 특정 요소에 접근할 때 시간복잡도는 O(N)이다. 

### 2. 삽입과 삭제
- 저장방식도 배열에서 요소들은 인접한 메모리 위치에 연이어 저장된다. 
- Linkedlist에서는 새로운 요소에 할당된 메모리 위치 주소가 linkedlist의 이전 요소에 저장된다.배열에서 삽입과 삭제는 O(N)이 소요되지만, Linkedlist에서 삽입과 삭제는 O(1)이 소요된다. 

### 3. 크기
- Array : 크기 고정
- LinkedList : 크기 동적

<br>
<br>
<details>
<summary>출처</summary>
1. https://medium.com/@audrl1010/linked-list-%EC%99%80-array-%EC%B0%A8%EC%9D%B4%EC%A0%90-4ba873c2e5f5<br>
2. https://devowen.com/285<br>
3. https://velog.io/@dion/difference-between-array-and-list<br>
4. https://www.geeksforgeeks.org/doubly-linked-list/
</details>

