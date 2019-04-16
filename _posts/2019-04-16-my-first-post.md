---
layout: post
title:  "우분투 단축키"
date: 2019-04-16
categories: Ubuntu
---
###### 참고 : <https://www.maketecheasier.com/useful-shortcut-keys-in-ubuntu/>
###### <https://soooprmx.com/archives/2777>

<br/>
# 유용한 단축키 모음

 아직 우분투가 익숙치 않아 단축키를 알아두면 작업할때 유용할것 같아서 포스팅하게 되었습니다. 익숙하지 않은 단축키 위주로 작성하였습니다.

---

<br/>
## Windows
#### *SUPER키는 WINDOW키와 동일하다*
- ALT + ` = 같은 프로그램의 다른 창 활성화
- CTRL + SUPER + UP = 창 최대화
- CTRL + SUPER + DOWN = 창 최소화 OR 최대화된 창 크기 복구
- ALT + SPACE = 창 메뉴 열기

## Screenshots
- PRTSC = 전체 화면 캡쳐
- ALT + PRTSC = 현재 활성화 된 창 캡쳐
- SHIFT + PRTSC = 마우스 선택 영역 캡쳐
- CTRL + PRTSC = 전체화면 캡쳐 후 클립보드에 저장
- CTRL + ALT + PRTSC = 현재 활성화 된 창 캡쳐 후 클립보드에 저
- CTRL + SHIFT + PRTSC = 마우스 선택 영역 캡쳐 후 클립보드에 저장

## Terminal
- CTRL + A = 첫 줄로 커서 이동
- CTRL + E = 마지막 줄로 커서 이동
- CTRL + C = 현재 프로세서 종료

- CTRL + Z = 현재 프로세서 백그라운드로 실행
- CTRL + D = 종료
- CTRL + R = 명령어 검색
- 글자 입력 후 TAB + TAB = 현재 문자로 실행 가능한 명령어 목록
- CTRL + U = 현재 줄 지우기
- CTRL + K = 커서가 위치한 곳 지우기
- CTRL + W = 커서 앞 지우기
- CTRL + L = 터미널 청소
- SHIFT + CTRL + C = 복사
- SHIFT + CTRL + V (or SHIFT + INSERT) = 붙여넣기
- ALT + F = 한 글자 앞으로 이동
- ALT + B = 한 글자 뒤로 이동
- 방향키 위/아래 = 사용한 명령어 확인
- SHIFT + PageUP/PageDown = 터미널 스크롤
  
---

<br/>
## vi 기본 사용법
### 커서 이동
- i = 현재 커서 위치에서 텍스트 삽입
- ESC = 명령모드 진입
- a = append. 현재 커서 위치 다음 글자부터 텍스트 삽입
- o = 현재 커서 바로 다음에 새 줄 추가 후 다음줄에서 바로 삽입모드로 전환
- SHIFT + o = 커서의 바로 위에 새 줄 추가

### 삭제(오려두기)
- x = 커서가 위치한 곳의 글자를 삭제
- d h = 커서가 위치한 곳에서 부터 한칸 앞을 삭제
 - d3h = 커서 위치로부터 3칸 앞의 글자들을 삭제
- d d = 현재 줄을 삭제
- d j = 현재 줄 포함하여 다음 줄까지 2줄을 삭제

### 고치기
- r = 현재 커서 위치의 한 글자 교체
- SHIFT + r = ESC를 누를 때까지 현재 줄의 내용 수정. 백스페이스 누를 시 기존 글자로 복구
- c = 커서위의 한 글자를 지우고 입력모드로 전환
- c w = 커서 위치부터 그 단어의 끝까지가 새로 입력한 글자로 대체
- SHIFT + s = 줄 전체를 새로 작성

### 복사 및 붙여넣기
- y = 복사 키, 이동 명령을 통해 복사 범위를 지정
- y w = 단어 끝까지 복사
- y $ = 현재 줄 끝까지 복사
- p = 붙여넣기

### 되돌리기
- u = 한 번의 변경을 되돌림
- SHIFT + u = 한 줄에 대해 변경사항을 모두 되돌림
- CTRL + r = 되돌린 내용을 다시 적용

### 저장 및 종료
- :cd = 현재 디렉토리 확인
- :cd _ PATHNAME _ = 다른 디렉토리로 변경

### 찾기 및 바꾸기
- / = 패턴 검색
- n = 다음 검색 결과로 이동
- SHIFT + n = 이전 검색 결과로 이동
- :%s/old/new = old를 찾아 new로 교체
- :%s/old/new/g = 전체를 검색하여 한 번에 모두 교체
- :%s/old/new/gc = 위와 동일하나 교체 시 마다 확인

### 도움말 사용하기
- :help = 도움말 시작, 분리된 창의 형태로 시작
- :help :cd = :cd명령에 대한 도움말 확인
