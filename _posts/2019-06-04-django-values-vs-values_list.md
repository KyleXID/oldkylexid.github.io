---
layout: post
title:  "장고 values()와 values_list()의 차이점"
date: 2019-06-04
categories: Django
--- 
## Django values() vs values_list()
- values()
  - 딕셔너리를 포함한 쿼리셋을 반환한다.
```python
Wecode.objects.values('야간반')
>>> <QuerySet [{'야간반':"min"}, {'야간반':"jun"}, {'야간반':"yeon"]>
```

- values_list()
  - 튜플로 이루어진 쿼리셋을 반환한다.
```python
Wecode.objects.values_list('야간반')
>>> <QuerySet [("min",), ("jun",), ("yeon",)]>
```
  - flat=True 옵션을 주면, 튜플이 아닌 하나의 값의 쿼리셋을 반환한다.
```python
Wecode.objects.values_list('야간반', flat=True)
>>> <QuerySet ["min", "jun", "yeon"]>
```
