##### 최지우 작성
<img width="437" alt="스크린샷 2021-02-09 오후 8 08 16" src="https://user-images.githubusercontent.com/29567741/107355241-8d59fb80-6b12-11eb-9601-a301e72adfb7.png">

## ArrayList와 LinkedList의 차이가 무엇인가요?

### 1. 공간적 제약
- ArrayList : 결국 배열이므로 길이가 고정되어 있습니다. 때문에, 새로 배열에 새로운 요소를 추가하려고 할 때, 배열의 용량이 이미 가득 차있다면 새로운 배열을 생성해주어야 합니다. 이 때, 새로 생성된 배열이 메모리 상에 연속해서 생길 수도 있지만, 이미 다른 값이 메모리를 사용하고 있는 경우, 새로운 위치에 배열이 생성되어야 하고 이는 모든 요소를 옮긴다는 얘기가 됩니다. 또 메모리에 여유공간이 없는 경우 에러가 발생할 수도 있습니다.

- LinkedList: 한 개의 Node는 다른 Node에 대한 참조만 가지고 있습니다. 따라서 공간적 제약을 ArrayList에 비해 받지 않습니다.

### 2. 새로운 요소 추가
- ArrayList : 새로운 요소를 추가할 때, 여유 공간이 있는 경우엔 O(1)이지만, 여유공간이 없는 경우엔 O(n)이므로 O(n)입니다.

- LinkedList : 새로운 요소를 추가할 때, 항상 O(1)입니다. 왜냐하면, 그냥 마지막 요소에서 다음 참조값을 가지게만 하면 되기 때문입니다.

### 3. 임의 접근과 순차 접근
- 임의 접근(Random Access) : 어떤 요소에 바로 접근하는 것. 
- 순차 접근(Sequential Access) : 어떤 요소에 접근할 때, 차례차례 접근하는 것.

- ArrayList :임의 접근, 바로 접근이 가능하다는 것은 곧 O(1)을 의미한다.
- LinkedList : 순차 접근만 가능, O(n)이 걸리게 됩니다.

### 4. 새로운 요소 삽입(중간에)
- ArrayList는 해당 요소뒤의 요소들도 전부 옮겨야 합니다.
- LinkedList는 앞 뒤 요소의 값만 바꾸어주면 됩니다.

### 5. 요소 삭제(중간에)
- ArrayList는 뒤의 요소들을 전부 앞으로 이동시켜야합니다.  
- LinkedList의 경우에는 앞 뒤 요소의 값만 바꾸어주면 됩니다.

## 요약

![스크린샷 2021-02-09 오후 8 10 58](https://user-images.githubusercontent.com/29567741/107355534-efb2fc00-6b12-11eb-90b0-364fa9f42600.png)



<br>
<br>
<details>
<summary>출처</summary>
1. https://medium.com/@audrl1010/linked-list-%EC%99%80-array-%EC%B0%A8%EC%9D%B4%EC%A0%90-4ba873c2e5f5<br>
2. https://devowen.com/285<br>
3. https://velog.io/@dion/difference-between-array-and-list<br>
4. https://www.geeksforgeeks.org/doubly-linked-list/<br>
5. https://www.nextree.co.kr/p6506/
</details>

