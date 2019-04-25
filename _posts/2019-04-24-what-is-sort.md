---
layout: post
title:  "What is sort?"
date: 2019-04-24
categories: Coding
---

## Sorting an Array

`sort()`는 배열을 정렬해주는 자바스크립트 내장 메서드이다.

<br/>
### arrayobj.sort(sortFunction)
`arrayobj`는 임의의 배열이다.  
`sortFunction`은 요소의 순서를 결정하는 데 사용되는 함수이다.  
오름차순, ASCII 순서로 정렬된다.

`sortFunction`은 `+`, `-`, `0` 3가지 값을 return 한다.  

- `+` : 첫번째 인수가 두번째 인수보다 클 경우
- `0` : 두 인수가 같을 경우
- `-` : 첫번째 인수가 두번째 인수보다 작을 경우

<br/>
`sort()`는 String타입과 Number타입 모두 정렬 가능하다.

<br/>
# String타입 정렬
 단순히 `sort()` 메서드만 쓰게 되면 자동으로 ASCII 문자 순서대로 정렬되어 나온다.  

<br/>
# Number타입 정렬
 숫자 정렬은 `sort()` 메서드에 추가 코딩을 해주어야한다.

```
let numarr = [5, 10, 3, 15, 1];

//오름차순
numarr.sort(function(a, b) {
  return a - b;
});
```

내림차순으로 바꿀경우 return의 a와 b의 순서를 바꾸어주면된다.
