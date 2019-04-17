---
layout: post
title:  "Function to output the longest non-duplicated alphabet"
date: 2019-04-17
categories: Coding
---

# CodeKata Review

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

 앞부분과 뒷부분을 `slice`로 나누어 앞문자열과 뒷문자열의 길이를 비교하였다.
이 후 앞문자열이 긴경우 뒷배열의 상황은 생각하지 않아도 되기 때문에 앞 문자열의 길이를 `return`하였다.

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
```

 이 코드는 뒷부분이 긴경우인 경우 실행되는 code이다.
문제점은 뒷부분에서 이렇게 코드를 읽어도 뒷문자열의 배열에 따라 결국 **무한하게 자르고 비교하는 행위**를 계속해야 한다는 것이다.
결국 접근 방법에 문제가 있다고 생각하여 계속 파트너와 feedback을 주고받다가 결국 시간초과로 coding을 멈추고 다른 작업을 하게되었다. 
