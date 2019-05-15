---
layout: post
title:  "이진 탐색(Binart Search)"
date: 2019-05-13
categories: Algorithm
---

## 이진탐색법(Binary Search)

*이진탐색과 선형탐색은 기본적으로 오름차순or 내림차순이 되어 있어야 적용할 수 있는 알고리즘이다.*

### 선형탐색
- list의 처음부터 마지막까지 차례대로 요소를 확인하며 찾으려는 요소가 나올때까지 반복하는 것.
 - 단점 : list의 길이가 길어지고, 요소가 시작지점에서 멀리있을 경우, 탐색을 여러번 해야함.

### 이진탐색
- 선형탐색의 단점을 보완하는 탐색.
- 중간 지점부터 찾아 나서는 탐색방법.
 - list의 중간index의 요소와 target의 크기를 비교하여 중간요소가 target보다 크면 왼쪽으로, target보다 작으면 오른쪽으로 이동하여 다시 이동한 지점의 중간index의 요소와 계속해서 탐색하는 방법이다.

![](/img/hhiR6QU.png)

```python
def search(nums, target):
  l, r = 0, len(nums) - 1
  while l <= r:
    mid = (l + r) // 2
    if nums[mid] < target:
      l = mid + 1
    elif nums[mid] > target:
      r = mid - 1
    else:
      return mid
  return -1
```
mid index에 +1 또는 -1 을 해주는 이유는 마지막 위치로 갔을 경우에 비교를 완료할 수 없기 때문이다.

