---
layout: post
title:  "Linked List"
date: 2019-05-17
categories: Algorithm
---
## 링크드 리스트란? 
-----------
#### 링크드 리스트는 각 node가 데이터와 포인터를 갖고 한 줄로 연결되어 있는 방식으로 데이터를 저장하는 자료 구조이다.

- node : 데이터상자. 주로 class로 구현된다.
- link : 각 데이터를 연결하여 리스트의 순서를 유지할 수 있게 해준다.

![](/img/linked.png) 

### Doubly Linked List

- Single Linked List와는 다르게 before의 노드의 link도 가지고 있는 리스트이다.
  - 리스트의 앞, 뒤 모두 이동이 가능하다.

### Circular Linked List

- List의 head와 tail이 연결되어 있는 리스트이다.
  - 리스트의 무한 반복이 가능하다.

### Array와의 차이

- 요소를 순차적으로 저장하나 차이점이 있다.
  - 배열은 인덱스가 있기 때문에 인덱스를 알면 바로 접근이 가능하다. 반면 링크드 리스트는 해당 위치로 가기위해서는 연결된 링크를 따라 차근차근 접근 해야 한다.

- Array는 물리적 주소가 순차적이고 링크드 리스트는 순차적이지 않다.
  - Array와 링크드 리스트는 데이터가 논리적 순서에 따라 순차적으로 입력된다는 공통점이 있다.

- Array는 데이터의 변화에 취약하다. 가장 마지막에 삽입될 경우에는 한번만 늘어나면 되지만, 그 외의 위치에 삽입 될 경우에는 그 다음부터 모든 데이터의 위치를 변경해야 하기 때문이다.
  - 링크드 리스트는 연결 주소만 바꾸어주면 되기때문에 간단하다.

- 같은 양의 데이터를 저장할 경우에 링크드 리스트가 Array보다 더 많은 메모리를 차지한다.
  - 링크드 리스트는 각 노드별로 객체를 생성해야하기 때문

### 언제 링크드 리스트를 사용하는가?

- 데이터의 양이 적고, 데이터의 변화가 빈번할 경우
 - 반대는 Array가 유리하다.


#### 다음은 싱글 링크드 리스트의 예제이다.

```python
class Node:
  def __init__(self,data):
    self.data   = data
    self.next   = None

class MyLinkedList(object):
  
  def __init__(self):
    self.head = None

  def print_list(self):  
    temp = self.head  

    while temp:
      temp = temp.next
    print("End")
      
  def get(self, index): #index번째 node의 value를 반환한다. 값이 없으면 -1을 반환.
    cur = self.head
    i   = 0
    
    while i != index:
      i += 1
      cur = cur.next
    
    if cur.data == None:
      return -1
    return cur.data

  def addAtHead(self, val): #리스트의 맨 앞에 value가 val인 node를 추가한다.
                            #이는 리스트의 head가 된다.
    newhead = Node(val)
    temp    = self.head
    
    self.head 	   = newhead
    self.head.next = temp
    
  def addAtTail(self, val):
    newtail = Node(val)
    
    cur = self.head
    
    while cur.next != None:
      cur = cur.next
      
    cur.next = newtail

  def addAtIndex(self, index, val): #리스트의 마지막에 value가 val인 node를 추가한다.
    cur = self.head
    i 	= 0
    
    if index == 0:
      self.addAtHead(val)
    
    while i != index-1:
      i += 1
      cur = cur.next
      
    if cur.next == None:
      self.addAtTail(val)
    else:
      new      = Node(val)
      new.next = cur.next
      cur.next = new
        
  def deleteAtIndex(self, index): #리스트의 index번째 node를 삭제한다.
      i   = 0
      cur = self.head

      if index == 0:
        self.head = self.head.next
        
      while i != index-1:
        i += 1
        cur = cur.next
        
      if cur == None:
        return -1
      
      cur.next = cur.next.next
 
  def reverseList(self, head): #리스트의 순서를 뒤집어서 반환한다.
      cur    = head
      before = None

      while cur != None:
        after = cur.next
    
        cur.next = before
        before = cur
    
        cur = after

      head = before
  
      return head
 
```
