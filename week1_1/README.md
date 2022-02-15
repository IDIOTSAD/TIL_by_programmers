# week 1_1

### ● 1강 요약 (안녕, 자료구조 & 알고리즘)
> * 자료구조를 왜 배워야 하는가?
> * 리스트가 아닌 어떤 자료구조를 만들면 시간을 줄일 수 있을까?
> * 결국 연산 시간을 줄이기 위한 고민에 대한 해결방안
> * 풀어야 하는 문제의 파악 후, 자료구조의 성질에 맞게 자료구조를 선택
> * 예) 최대값은 정렬하면 찾기가 쉬워짐.
> * 이를 위해서 다양한 알고리즘을 많이 사용함.

### ● 2강 요약 (선형 배열)
> * 선형배열은 일렬로 늘어진 자료형이다. 원소들을 순서대로 정렬해놓음.
> * 대표적으로 리스트가 있다. (배열보단 융통성 있는 자료형)
> * 리스트는 어떠한 자료형이라도, 각 원소의 길이가 달라도 사용할 수 있음.
```
  원소 추가 = .append(원소)
  마지막 원소 제거 = .pop() -> 파라메터가 필요 없음.
  해당 함수의 시간복잡도 : O(1)

  원소 위치 지정 후, 직접 삽입 = .insert(원소 위치 주소)
  원소 위치 지정 후, 직접 삭제 = .del(원소 위치 주소)
  원소 위치 탐색 .index(원소 내용)
  해당 함수의 시간복잡도 : O(1) ~ O(N) -> 맨 끝에서 맨 앞까지
```
### ● 3강 요약 (정렬, 탐색)
> * 파이썬 리스트 정렬 방법
> * 파이썬 내장 함수 = sorted(리스트, 오름차수여부(reverse), key=lambda x: 조건)
> * 만약, 람다를 x['딕셔너리 이름'] 같이 정하면, 딕셔너리에서 해당 이름을 정렬 가능
> * list 함수 = .sort()

* 탐색 알고리즘
```
  1. 선형탐색 -> 리스트 순서대로 찾는 방법 -> 시간복잡도 : O(N)
  2. 이진탐색 -> 리스트가 정렬 되어있을 때 사용
  -> 중간값 비교해서 대상이 작으면 왼쪽으로 줄이고, 크면 오른쪽으로 줄임.
  -> 시간복잡도 O(log N)
```
### ● 4강 요약 (재귀 알고리즘)
> * 재귀 = 하나의 함수에서 자신을 다시 호출하여 작업을 수행하는 것.
> * 이진 탐색의 경우, start와 end의 변화된 부분을 계속 값을 주고 같은 함수로 돌림.
> * 예시) 1~n 까지 더하는 문제는 현재 n과 n-1까지의 더한 값을 더하면 1~n까지의 합임. -> 시간복잡도 O(N)
> * 이를 활용하여 점화식을 세워서 풀면 됨. 재귀는 종료 조건이 필수임.
> * 재귀의 효율은 N이 커질수록 함수호출이 많아지므로 효율은 좋지 못함.

### ● 5강 요약 (재귀 알고리즘 응용)
> * ![image](https://user-images.githubusercontent.com/55529455/154016554-e04a0921-58b5-4fc9-9c5a-d267417106d0.png) -> 조합계산을 구현 (n개의 각각 다른 원소에서 m개 선택)
> * from math import factorial as f 를 이용하여 ![image](https://user-images.githubusercontent.com/55529455/154016780-d83aeb67-3c57-48b8-80e2-34f3e412be0f.png) 로 구현
* n개의 각각 다른 원소에서 m개 선택하는 경우의 수
> * ![image](https://user-images.githubusercontent.com/55529455/154017079-2246c6f9-6f12-4c78-a6ab-8466e8f80ea3.png)로 표현이 가능함.
> * 따라서 다음과 같은 점화식을 내릴 수 있음. 
> * ![image](https://user-images.githubusercontent.com/55529455/154017666-bc76a0b8-ef33-4383-85b9-e504a7eceb46.png)

### ● 6강 요약 (알고리즘의 복잡도)
> * 시간 복잡도 = 문제의 크기와 이를 해결하는데 걸리는 시간의 관계
> * 공간 복잡도 = 문제의 크기와 이를 해결하는데 소요되는 메모리 크기의 관계
> * 평균 시간 복잡도 = 임의의 입력 패턴을 가정했을 때 소요되는 시간의 평균
> * 최악 시간 복잡도 = 가장 긴 시간을 소요하게 만드는 패턴을 입력함에 따라 소요되는 시간
> * 빅오 = 접근 표기법의 하나, 다른 함수와의 비교로 표현, 시간 복잡도.
```
예시) 선형 시간 알고리즘 = O(n) => 평균, 최악 둘다 같음.
예시) 이진 탐색 알고리즘 = O(log n)
예시) 삽입 정렬 = 최선(정순 정렬) => O(n),  최악(역순 정렬) => O(n^2)
예시) 머지 정렬 = O(n log n) -> 정렬 문제는 이거보다 더 낮은 복잡도는 없음.
-> 반씩 나누면서 1개로 나눈다. -> O(log n)
-> 1개씩 정렬된 원소를 2종류로 합치고, 골라가며 작은수를 뽑는다 -> O(n)
```


### ● 7강 요약 (연결 리스트)
> * 추상적 자료구조
> * 데이터 = 정수, 문자열, 레코드 등
> * 작업의 집합 = 삽입, 삭제, 순회, 정렬, 탐색 등 -> 추상적으로 보이는게 추상적 자료구조
> * 연결리스트 - 자료를 담는 데이터와 다음 주소가 담긴 링크로 구성됨. -> ![image](https://user-images.githubusercontent.com/55529455/154018219-75df447f-a2fa-4e2a-ab48-5194f5572109.png)

```
class Node:
    def __init__(self, item):
        self.data = item
        self.next = None
```

> * 머리, 꼬리, 연결리스트 개수를 담은 클래스를 만드는것이 좋다. ![image](https://user-images.githubusercontent.com/55529455/154018317-26462f41-6bcb-4ee4-857f-16f6f698e482.png)

```
class LinkedList:
    def __init__(self):
        self.nodeCount = 0
        self.head = None
        self.tail = None
```
> * 배열과 연속리스트의 차이점
> * 배열 - 연속한 위치로 저장되고, 이로 인해 간단하게 인덱스 찾기 가능 - O(1)
> * 연결리스트 - 임의의 위치로 저장이 되기 때문에, 선형탐색으로 인덱스를 찾아야 함. - O(n)

### ● 8강 요약 (연결 리스트)
> * 연결리스트 노드삽입 - insertAt(self, pos, newNode) pos의 위치는 1보다 크고 총개수+1 -> 그 사이에 삽입하여 성공 실패 여부 확인
> * 연결리스트 삽입 방법
```
연결 시 -> 새로운 노드의 방향에 앞쪽 노드 가리키게 하고, 이전 노드의 방향을 새로운 노드를 가리키게 하고, 카운트 증가로 코딩.
하지만, 맨 앞과 맨 끝일때는 코드가 달라짐.
맨 앞 -> prev없이 새로운 노드 방향을 이전 head로 하고, head 부분만 새로운 노드로 조정하면 됨. + 카운트 증가
맨 뒤 -> prev를 예전 tail로 지정하여 방향을 새로운 노드로 가리키고, tail 부분을 새로운 노드로 조정하면 됨. + 카운트 증가
연결리스트 삽입 시간 복잡도 = 맨앞, 맨뒤는 O(1), 중간은 O(n)
```
> * 연결리스트 삭제 방법
```
삭제 시 -> 이전 노드의 prev로 정하고, 방향을 자신의 방향으로 변환하고, 현재 위치의 노드를 삭제함. 카운트 감소
맨 앞 -> prev 없이 head를 다음 노드로 바꾸고, 현재노드 삭제
맨 뒤 -> prev를 tail 이전 노드로 지정하고, tail 삭제 후, prev를 tail로 지정.
pos == nodeCount 면? 한번에 할 수 없음. prev, 이전 값이 없음. 따라서 앞에서 찾아야함.
삭제 = 맨 앞 시간복잡도 - O(1), 중간 시간복잡도 - O(n), 맨 끝 시간복잡도 O(n)
```
> * 2개의 연결리스트 연결 방법
```
두 리스트의 연결 -> 왼쪽 리스트의 끝의 방향(next)을 오른쪽 리스트의 머리로 연결하고, 오른쪽 리스트의 끝을 왼쪽 리스트의 tail로 지정함.
그리고, 각각의 카운트를 합쳐야함. 하지만, 합칠 리스트가 비어있는지 검사해야함.
```
### ● 9강 요약 (연결 리스트)
> * 연결리스트의 최고 장점 = 삽입과 삭제가 유연하다는 장점. 하지만, 매번 할 때마다 이전 노드를 찾으러 떠나야하는 단점이 있음.
> * 연결리스트의 최고 장점을 살리는 방안으로 dummy node를 추가함으로써 코드의 재사용을 추구할 수 있음. 
```
연결 리스트 초기화 시, dummy node 추가.
class LinkedList:

	def __init__(self):
		self.nodeCount = 0
		self.head = Node(None)
		self.tail = None
		self.head.next = self.tail
```
> * 리스트 순회의 경우 다음과 같이 변경할 수 있음.
```
    def traverse(self):
        result = []
        curr = self.head
        while curr is not None:               ->  while curr.next:
            result.append(curr.data)          ->      curr = curr.next
            curr = curr.next                  ->      result.append(curr.data)
        return result
```
> * 리스트 참조의 경우 다음과 같이 변경할 수 있음.
```
    def getAt(self, pos):
        if pos < 1 or pos > self.nodeCount:	->	if pos < 0 or pos > self.nodeCount:
            return None

        i = 1					->	i = 0
        curr = self.head
        while i < pos:
            curr = curr.next
            i += 1

        return curr
```
> * 삽입 할 때, 이전 노드를 알 수 있으면 다음 메서드를 적용 할 수 있음.
```
	def insertAfter(self, prev, newNode):
		newNode.next = prev.next
		if prev.next is None:
			self.tail = newNode
		prev.next = newNode
		self.nodeCount += 1
		return True
```
> * 기존의 삽입부분의 메서드 또한 변경 되어야 함.
```
* 변경 이전
    def insertAt(self, pos, newNode):
        if pos < 1 or pos > self.nodeCount + 1:
            return False

        if pos == 1:
            newNode.next = self.head
            self.head = newNode

        else:
            if pos == self.nodeCount + 1:
                prev = self.tail
            else:
                prev = self.getAt(pos - 1)
            newNode.next = prev.next
            prev.next = newNode

        if pos == self.nodeCount + 1:
            self.tail = newNode

        self.nodeCount += 1
        return True
```
> * 위에 구현된 insertAfter 함수를 호출하여 사용하면 간편해짐.
> * pos 범위 조건 확인
> * pos == 1, head 뒤에 새로운 node 삽입
> * pos == 개수 + 1 인 경우, prev(이전 노드)가 tail이 됨.
> * 그렇지 않으면, getAt 함수를 통해서 참조한 이전 노드를 insertAfter 함수로 전송.
```
* 변경 후
	def insertAt(self, pos, newNode):
		if pos < 1 or pos > self.nodeCount + 1:
			return False

		if pos != 1 and pos == self.nodeCount + 1:
			prev = self.tail
		else:
			prev = self.getAt(pos - 1)
		return self.insertAfter(prev, newNode)
```
> * 노드 삭제의 경우는 prev의 링크는 curr의 링크를 가리키게 하면 된다.
> * 단, prev가 마지막 node 이면, 삭제할 node가 없으므로 None을 반환해야함.
> * 또한, 리스트 맨 끝의 node 를 삭제 할 때는 tail의 조정만 있으면 됨.
> * popAfter, popAt을 통해서 구현 가능함. 위의 예외 사항을 확인하여 구현한다.

### ● 10강 요약 (양방향 연결 리스트)
> * 양방향 연결리스트는 연결리스트들이 이전노드와 다음노드를 가리키는 2개의 링크로 연결되어 있음
> * 장점 = 앞, 뒤로 방문이 가능하므로 작업할 때 유리한 점이 있다.
> * 단점 = node에 link가 추가되므로 메모리의 양이 늘어나는 점이 있다.
> * 유의 사항으로는 link가 늘어난 만큼, 삽입, 삭제 등 변화가 일어 날 때, link를 한번 더 잘 연결 해주어야 한다.
> * 하지만, 이로 인해 예외사항이 많이 없어짐.

* 양방향 연결리스트의 node 구성
```
class Node:

    def __init__(self, item):
        self.data = item
        self.prev = None
        self.next = None

```

* 양방향 연결리스트의 구성 -> 이 때, link가 늘어난 만큼, 초기화 할 값도 늘어나게 됨.
```
class DoublyLinkedList:

    def __init__(self):
        self.nodeCount = 0
        self.head = Node(None)
        self.tail = Node(None)
        self.head.prev = None
        self.head.next = self.tail
        self.tail.prev = self.head
        self.tail.next = None
```
