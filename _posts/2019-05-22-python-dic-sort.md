---
layout: post
title:  "파이썬에서 딕셔너리 정렬하기"
date: 2019-05-22
categories: Python
---
## 딕셔너리 정렬
----------
<br/>
### 1.Key를 기준으로 정렬하기
-------
<br/>
```python
>>> sort(dic)
```
을 해주면 dic 안의 key를 올림차순으로 정렬한 리스트를 반환해준다.

이때 key가 아닌 value로 정렬하려면 lambda를 사용해주면 된다.

```python
>>> sorted(dic, key= lambda x : dic[x])
```
를 해주면 value값을 기준으로 정렬한 리스트를 반환해 준다.
내림차순은 `reverse = True`라는 옵션을 뒤에 붙여주면 된다.

### 2.items() 정렬
-------
딕셔너리에 .items() 메서드를 사용해주면 `key : value`의 형태를 `(key, value)`의 형태로 바꿔서 list를 만들
어 준다.
이를 sorted해주면 key값을 기준으로 오름차순으로 정렬해준다.
value값으로 정렬하려면 lambda를 사용해주면 된다.

```python
>>> sorted(dic.items(), key=lambda x : x[1])
```
위에서 사용한 lambda와 아래 사용한 lambda의 차이를 인지하자.

위는 딕셔너리에 접근하였고, 아래는 튜플에 접근하여 사용하기때문에, 해당 value값이 위치한 곳에 접근하기 위
함임을 알아두어야 한다.


### 3.itemgetter를 사용한 정렬
-----------
파이썬에서 제공하는 itemgetter를 사용하여 딕셔너리를 정렬 할 수 있다.

```python
from operator import itemgetter
dic = {'wecode':1, 'ryan':2, 'wework':3}
sortdic = sorted(dic, key = itemgetter(0))
>>> sortdic = {'wecode':1, 'wework':3, 'ryan':2}
```
`itemgetter`안에는 키값이 들어갈수도 있고, 인덱스를 넣어줄수도 있다.  
위의 예제는 0번쨰 인덱스 즉, 정렬기준은 key자체가 된다.  
먄약 인자를 1로 바꿔주면
```python
>>> sortdic = {'wecode':1, 'ryan':2, 'wework':3}
```
으로 나올 것이다. 인자1은 value 기준에 따라 오름차순으로 정렬해 준다.  
`itemgetters`는 안에 하나이상의 값이 들어가면 먼저 기준에 따라 정렬하고, 동일한 값이 나올 경우 다음 기준으로 다시 정렬한다.  
마지막에 옵션으로 `reverse=True`를 해주면 내림차순으로 정렬이 된다.

#### 응용
```python
from operator import itemgetter
  
                .
                .
                .
    total_hearts_list = [
	{
		"img_id"       : d['pk'],
                "total_hearts" : Cloth.objects.get(id = d['pk']).total_hearts
	} for d in hearts_list
    ]
    data = sorted(total_hearts_list, key = itemgetter('total_hearts'))                      
```
  
`total_hearts_list`라는 list에서 key가 `totla_hearts`인 값들을 오름차순으로 정렬한 code이다.    
`itemgetter`에는 하나 이상의 값을 넣어서 순서대로 정렬시킬 수 있다.   
