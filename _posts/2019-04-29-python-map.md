---
layout: post
title:  "Python map()"
date: 2019-04-29
categories: Python
---
## 파이썬 map()함수
---------
## 파이썬 내장함수 map()  

파이썬에는 내장함수 map()이 존재한다. map()은 두개의 인자를 받는 함수이며, 첫번째인자는 함수, 두번째 인자는 리스트 또는 딕셔너리와 같은 iterable한 데이터를 인자로 받는다.

  
예시)
  
```python
>>> def myfunc(n):
...   return len(n)
  
>>> x = map(myfunc, ('apple', 'banana', 'cherry'))
['5', '6', '6']
```
`map()`은 `myfunc`이라는 함수를 반복적으로 모든 인자에 수행한 후 그 결과를 `return` 한다.                             

다음과 같이 사용할 수도 있다.  

```python
>>> a1, a2 = map(int, a[:-1].split('+'))
>>> b1, b2 = map(int, b[:-1].split('+'))
```

이는 각 `split`하고 `slice`한 배열 a1,a2를 `int`라는 함수를 반복적으로 적용하여 data type을 number로 반환해 준다.

간단하고 굳이 재사용할 함수가 아니라면 lambda를 이용하여 좀더 코드를 줄일 수 있다.

```python
>>> a = [3, 5, 7]
>>> b = [1, 3, 5]
>>> list(map(lambda x, y : x * y, a, b))
[3, 15, 35]
```
