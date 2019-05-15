---
layout: post
title:  "버블 정렬(Bubble Sort)"
date: 2019-05-15
categories: Algorithm
---
## 버블 정렬(Bubble Sort)

버블 정렬은 인접한 데이터를 교환해서 정렬하는 알고리즘이다.  
알고리즘의 정렬되는 모습이 마치 거품처럼 보인다고 해서 붙여진 이름이다.  

![](/img/bubble.gif)  

![](/img/bubblepass.png)  

**선택 정렬과 차이점**
- 버블 정렬은 바로 옆 index의 요소와 크기를 비교하여 자리를 바꿔주면서 정렬을 해나가는 방법이다.
- 선택 정렬은 list의 최대값을 먼저 찾고 이 값을 차례대로 정해진 위치로 보내는 방법이다.

- 비교 횟수 측면 : 버블 정렬과 선택 정렬이 동일
- O(n^2)의 계산 복잡성을 포함
- 자리 이동 측면(swap) : 선택 정렬이 효율적(버블 정렬은 swap을 해나가면서 위치를 이동하기 때문)ㅑ

- 장점 : 구현이 간단하다.
- 단점 : 자리 이동 측면에서 비효율적이다.  
&nbsp;&nbsp;&nbsp;&nbsp;특정 요소가 최종 정렬 위치에 이미 있는 경우라도 교환되는 일이 발생한다.

```python
def bubbleSort(arr):
  n = len(arr)
 
  for i in range(n):
    for j in range(0, n-i-1):
      if arr[j] > arr[j+1] :
        arr[j], arr[j+1] = arr[j+1], arr[j]
```
