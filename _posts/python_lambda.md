---
layout: post
title:  "Python lambda"
date: 2019-05-22
categories: Python
---
## Python 람다(lambda)
------------
lambda는 일시적인 함수이며, 간단하게 함수를 한줄로 표현하여 정의해 두고 쓰는 것이 아닌, 필요할때 바로 사용하는 함수이다.

람다는 다음과 같이 써줄 수 있다.

### 기본 사용
```python
lambda 인자 : 표현식
```

### 예제
```python
>>> test = lambda x:x**2
>>> print(test(5))
5

>>> (lambda x, y: x + y)(3, 5)
8
```

딕셔너리 정렬에도 사용된다.

### 활용 : dic sort
```python
sorted(dic, key=lambda k : dic[k], reverse=True)
```

### 활용 : map()

map함수는 과거 포스팅에서 한번 정리한적이 있다.
맵 함수는 두개의 인자를 받는 함수이며, 여기에 lambda를 적용시킬 수 있다.

```python
>>> a = range(3)
>>> b = [1, 3, 5]
>>> list(map(lambda x, y : x * y, a, b))
[0, 3, 10]
```

### 활용 : filter()
filter는 두개의 인자를 받으며 첫번째 함수를 만족하는 두번쨰 원소들로 새로운 리스트를 만들어주는 함수이다.

```python
>>> x = [0, 1, 3, 101, 5, 2]
>>> filter(lambda a: a<=3, x)
[0, 1, 3, 2]
```
### 활용 : reduce()
reduce는 순서형 자료(문자열,리스트,튜플)의 원소들을 누적하며 마지막 요소까지 함수를 돌리는 함수이다.

```python
>>> from functools import reduce
>>> a = [1, 3, 5, 7]
>>> reduce(lambda x, y : x * y, a)
105
```
이는 `((1 * 3) * 5)* 7`을 하는 것과 동일하다.


