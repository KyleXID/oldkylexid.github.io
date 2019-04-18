---
layout: post
title:  "Function to output the longest non-duplicated alphabet"
date: 2019-04-17
categories: Coding
---

# CodeKata Review
---
<br/>
 **오늘 CodeKata는 문자열을 받아 그 중 중복되지 않은 알파벳으로 이루어진 제일 긴 단어의 길이를 반환하는 함수를 만드는 주제였다.**

 일단 나의 접근 방법은 일정한 문자 배열을 받을 경우 해당 위치에서 앞부분과 뒷부분으로 나누어 문자를 생성한 뒤 이 부분을 각 변수에 할당하여 각 변수를 비교하는 것으로 접근하였다.

```
function getLengthOfStr(str) {
  if (str.length === 0) {
    return 0;
  } else {
    for(let i = 0; i < str.length; i++) {
      for(let j = i+1; j < str.length; j++) {
        if(str[i] === str[j]) {
          let frontstr = str.slice(0, j);
          let behindstr = str.slice(j, str.length);
  
          if(frontstr.length > behindstr.length) {
            return frontstr.length;
			.
			.
			.
```

*앞부분과 뒷부분을* `slice`*로 나누어 앞문자열과 뒷문자열의 길이를 비교하였다.*  
이 후 앞 문자열이 긴경우 뒷배열의 상황은 생각하지 않아도 되기 때문에 앞 문자열의 길이를 `return`하였다.

<br/>
 **하지만 이 코드의 문제점은 뒷부분에서 나타났다.**

```
if(frontstr.length > behindstr.length) {
            return frontstr.length;
          } else {
            for(let i = behindstr.length-1; i >= 0; i--) {
              for(let j = i-1; j > 0; j--) {
                if(behindstr[i] === behindstr[j]) {
                  let okend2 = behindstr.slice(j+1, behindstr.length);
                  let okend1 = behindstr.slice(0, j+1);
                  if(okend1.length > okend2.length) {
                    return okend1.length;
                    } else {
                      return okend2.length;
			     .
			     .
			     .
```

 이 코드는 뒷부분이 긴경우인 경우 실행되는 code이다.  
문제점은 뒷부분에서 이렇게 코드를 읽어도 뒷문자열의 배열에 따라 결국 **무한하게 자르고 비교하는 행위**를 계속해야 한다는 것이다.
결국 접근 방법에 문제가 있다고 생각하여 계속 파트너와 feedback을 주고받다가 결국 시간초과로 coding을 멈추고 다른 작업을 하게되었다.
<nb/>
<nb/>
## Code feedback
--- 
<nb/>
이후 멘토에게 코드 피드백을 받았다.

**멘토의 모범답안**
```
function getLengthOfStr(s) {
    let strArr = [];
    let prevStrArr = [];

    for (let i = 0; i < s.length; i++) {
        let ss = s.slice(i, i+1);
        for (let j = 0; j < strArr.length; j++) {
            if (ss === strArr[j]) {
                
                if (prevStrArr.length < strArr.length) {
                    prevStrArr = strArr.slice();
                }
                
                strArr = strArr.splice(j+1, strArr.length);
                break;
            }
        }
        
        strArr.push(ss);
    }
    
    return Math.max(strArr.length, prevStrArr.length);
}

console.log(getLengthOfStr('taaaytts'));
```
*각 문자열을* ```slice```*로 잘라 빈 배열에 계속 추가하고 같은 문자열을 만났을때 상황을 정리한 code*
<nb/>
멘토의 코드를 위부터 차근차근 살펴보자.  
먼저 멘토는 빈 배열을 선언하였다.  
<nb/>
후에 ```for```문을 통하여 각 문자를 ```slice```로 자른 뒤 ss에 선언한다. ss를 ```strArr[]```의 각 배열과 비교하여 아무것도 일치하는것이 없는 경우 ```strArr```배열에 ```push```한다.  
<nb/>
만약 ```for```문을 돌면서 값이 일치하는  경우에는 ```prevStrArr```배열의 길이와 ```strArr```배열의 길이를 비교하여 ```prevStrArr```의 배열의 길이가 작을경우에는 ```strArr```의 배열을 ```prevStrArr```에 넣어준다.
<nb/>
<nb/>
**여기서 ```strArr```의 배열을 ```prevStrArr```의 배열에 넣어줄 때 ```slice```를 쓴 이유는 무엇일까?**  
>**Array** 는 배열 값 자체가 저장되는 것이 아니라, 그 배열의 참조값이 저장되기 때문이다.  
>이를 빠르게 이해하기 위해서 ```let a = [1, 2, 3]``` 과 ```let b = [1, 2, 3]``` 이 동일한지 확인하자  
>결과는  **false**가 나올것이다.
<nb/>
그렇기 때문에 만약 ```prevStrArr = strArr``` 처럼 값을 저장하게 되면, 후에 ```strArr```의 배열이 바뀔때마다 ```prevStrArr```의 값도 동일하게 바뀔것이다.  
>*이는 ```prevStrArr```에 strArr배열 값이  저장된 것이아니라,  
>```strArr```의 참조값을 할당받기  때문이다*  
<nb/>
이를 피하기위해 ```slice()```형식으로 변수값을 저장해주면 ```prevStrArr```에 다른 reference로 배열이 저장되어 독립적인 배열을 갖게된다.
<nb/>
이후에는 ```strArr```이 ```ss```와 중복된 값이 마주친 곳에서부터 ```splice```하여 함수를 돌려주게 된다.  
그 후 ```Math.max```함수를 이용하여 가장 길이가 긴 값을 ```return```하게 되면서, 중복되지 않은 알파벳으로 이루어진 제일 긴 단어의 길이를 반환하게 되는 ```function```이 완성된다.
