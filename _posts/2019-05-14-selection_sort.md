---
layout: post
title:  "선택 정렬(Selection Sort)"
date: 2019-05-14
categories: Algorithm
---
## 선택 정렬(Selection Sort)

정렬 알고리즘은 무작위인 데이터를 순서대로 배치하는 알고리즘이다.

정렬의 방법에는 대표적인 알고리즘 4개가지가 있다.
- 선택 정렬
- 버블 정렬
- 삽입 정렬
- 퀵 정렬

이번 포스팅에서 다루는 선택 정렬은 list의 가장 크거나 작은 값을 정해진 위치로 차례 대로 보내서 list를 정렬하는 방법이다.  

![](/img/selectionsortnew.png)

<br/>

**버블 정렬과 차이점**
- 버블 정렬은 바로 옆 index의 요소와 크기를 비교하여 자리를 바꿔주면서 정렬을 해나가는 방법이다.
- 선택 정렬은 list의 최대값을 먼저 찾고 이 값을 차례대로 정해진 위치로 보내는 방법이다.

- 비교 횟수 측면 : 버블 정렬과 선택 정렬이 동일
- O(n^2)의 계산 복잡성을 포함
- 자리 이동 측면(swap) : 선택 정렬이 효율적(버블 정렬은 swap을 해나가면서 위치를 이동하기 때문)

```python
def selectionSort(nums):
  for i in range(len(nums)): 
    min_idx = i 
    for j in range(i+1, len(nums)): 
      if nums[min_idx] > nums[j]: 
          min_idx = j 
              
    nums[i], nums[min_idx] = nums[min_idx], nums[i] 
    
  return nums
```
