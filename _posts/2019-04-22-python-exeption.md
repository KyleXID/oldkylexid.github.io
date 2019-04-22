---
layout: post
title:  "How python access to sys.modules"
date: 2019-04-22
categories: Python
---
파이썬은 변수나 함수, 클래스와 같은 것들을 모듈에 저장해놓습니다.
그 이유는

> - 다른 파일에서 재사용하기 위해서
> - 전체 코드가 한 파일에 넣기에는 커져서 여러 파일로 나누어서 정리하기 위해서

<br/>

파이썬은 모듈과 패키지를 사용하기 위해서 **Import**를 해주어야 합니다.

일반적으로 Import는 `sys.modules` - `built-in modules` - `sys.path` 의 장소를 순서대로 탐색합니다.

<br/>
**sys.modules**  
`sys.moudles`는 한번 import된 모듈과 패키지를 저장하고 있는 dictionary입니다.
`sys.moudles`을 사용하려면 import를 해주어야합니다.  
*새로 import 하려는 모듈은* `sys.modules`*에서 찾을 수 없습니다.*

<br/>
**built-in modules**  
파이썬에서 제공하는 파이썬 공식 라이브러리를 모아둔 모듈입니다.

<br/>
**sys.path**  
`sys.path`는 각 경로를 저장하고 있는 list입니다. 파이썬은 각 경로들을 하나 하나 확인하며 패키지/모듈을 탐색 합니다.

---

<br/>
# **그렇다면 sys.moudles을 Import할때 python은 어디서 모듈위치를 찾을 수 있을까?**
`sys.moudles`는 python에서 제공하는 module로 built-in에 포함되어있습니다.  
이 모듈을 Import할 경우 python은 `built-in moudules`에 접근하여 `sys.modules`를 불러옵니다. 
