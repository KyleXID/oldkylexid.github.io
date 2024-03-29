---
layout: post
title:  "Sorting JavaScript Object by property value"
date: 2019-04-25
categories: JavaScript
---

## 객체(object) 정렬하기
자바스크립트는 기본적으로 배열을 정렬하는 기능을 포함하고있다.

`sort`라는 매서드를 호출하면 배열을 간단하게 정렬할 수 있다.

```javascript
let test = [1,4,2,10,3];

test.sort();
//결과 : [1,2,3,4,10]
```
오름차순으로 정렬하고 싶으면 `.reverse()`를 이용하면 된다.

하지만 객체는 `sort`를 쓴다고 해서 바로 정렬이 되지않기 때문에, `sort`에 추가 coding을 해주어야한다.

# 객체를 value값에 따라 key값과 함께 정렬
```javascript
let testobj = { "1": 5
  "2": 3
  "5": 1
};

let sortobj = [];
for (let number in testobj) {
  sortobj.push([number, testobj[number]]);
}
sortable.sort(function(a, b) {
  return a[1] - b[1];
});
```

이 방법을 쓰면 내림차순으로 다시 재정렬된 값을 볼 수 있다.  
오름차순으로 정렬하려면 반환되는 값을 `b[1] - a[1]`로 순서를 바꿔주면 된다.

<br/>
정렬된 key값만 추출하는 간단한 방법도 존재한다.
```javascript
let keysSorted = Object.keys(testobj).sort(
  function(a,b){
  return numi[a]-numi[b];
  }
);
//keySorted = 5,2,1
```
