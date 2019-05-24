---
layout: post                   
title:  "재귀(Recursion)"
date: 2019-05-16
categories: Algorithm          
---
## 재귀(Recursion)
-------------
재귀는 알고리즘은 아니지만, 알고리즘 문제를 풀 때 자주 사용되는 프로그래밍 패턴이라고 배워서 정리하게 되었다.

- 함수 실행 내부에서 다시 함수 자신을 호출하는 것을 재귀라고 한다.
  - 다시 자신을 호출하면서 코드가 무한 반복이 되기 때문에, 적절한 조건과 걸어두어, 필요한 만큼 반복 후 return 될 수 있도록 만든다.

- codekata나 다른 예제들을 참고하여 자주 눈에 익히는 것이 좋을 것 같다.

#### 재귀를 사용한 코드카타. string을 인자로 받을 때 reverse해서 출력하는 재귀함수를 구현하였다.
```python
def reverseString(str):
  if len(str) == 0:
    return ''
  else:
    str = list(str)
    a = str.pop()
    str = ''.join(str)
    return a+reverseString(str)

print(reverseString('hello'))
```
- 다른 방법
```python
def reverseString(str):
  if len(str) == 0:
    return str
  else:
    return reverseString(str[1:]) + str[0]
```
