---
layout: post
title:  "Git rebase"
date: 2019-05-22
categories: GitHub
---
## git rebase 정리
----------------

### github를 이용해서 push하기 전에 항상 체크해야 할 사항
- git status를 해서 현재 어떤 파일이 변동사항이 있는지(커밋이 되고있는지) 확인해야함.
  - 본인이 원치않는 파일 확인하기위해서
- status로 확인 후 git diff를 통해서 원하는대로 변화가 이루어져 있는지 확인한다.
  - 이때, 불필요한 코드가 들어있는지 확인해주도록 한다.*ex)테스트를 위해 사용한 print문*

### git 명령어 remind
- git add -A or git add . : 현재 변동사항 모두 업로드.
- git add -u : 이미 git에 포함된 파일만 업로드 해준다.
- tig : 현재 branch와 master 상황 시각화.
- gc : git commit (이와 비슷한 줄임명령어가 몇몇 존재한다.)

### git rebase는 왜 해주는걸까?

#### 1.wip(Work in progress)
- 일반적으로 branch를 checkout한 후에 작업을 할때 작업이 생각보다 길어지는 상황이 올 때가 있다. 이때 작업사항을 중간중간 저장할때 commit을 하게 되는데, 아직 작업이 끝난 상황이 아니므로 wip로 간단하게 commit메세지를 날리게 된다.
- 이렇게 의미가 없는 commit메세지들이 쌓이게 되고, 이를 push하면 굉장히 지저분해 보일 수 있다.
- 이렇게 실질적으로 의미가 없는 메세지들을 하나로 합쳐서 깔끔하게 해줄 수 있다.

#### 2.commit은 시간순서이다.
- 팀원과 협업을 할때 서로 다른 branch에서 commit을 쌓아가며 작업을 했다고 가정하자. 이때 push를 팀원1, 팀원2 순서대로 push를 할 때 commit 메세지는 어떻게 쌓일까?
- 일반적으로 branch가 달라서 서로 다르게 쌓일꺼라고 착각할 수 있지만, commit한 시점의 시간대에 따라 서로 branch가 섞여서 쌓이게 된다.
- 즉, commit이 쌓이는 기준은 commit한 시간기준이지, branch기준이 아니라는 것이다.
- 이렇게 되면 master branch에 쌓일 때 가독성이 떨어지고, 만일의 경우에 해당 commit으로 돌아가려고 할때 곤란할 수 있다.
- 이를 피하기위해 마지막에 commit을 하나로 합쳐서 작업을 끝내는 것이 좋다.

#### 3. 단점
- 기존의 작업에서 계속 해나간 commit들이기 때문에 conflict가 겹쳐서 날 수 있음
- 이를 피하기위해 master에서 최신 pull을 받아서 할 경우 단점
  - 중간중간 수정한것까지 squash를 해줘야 하고, history가 더러워진다.
  - 완벽하게 완료한 프로젝트면 상관이 없겠지만, 미완성일 경우 마스터에서 합쳐져서 되돌릴 수 없게 된다.

### git rebase 사용하기

- `git rebase -i mater` : 마스터를 상대로 리베이스하는 커맨드이다.
  - i : interactive의 약자
- 위 커맨드를 실행해주면, 내가 여태해왔던 commit 메세지들을 보게되고 아래에는 자세하게 옵션 설명이 되어있다.
- 여기서 실질적으로 사용할건 pick과 s(squash)이다.
  - squash옵션을 받은 메세지는 상단의 commit에 합쳐진다.(상단의 commit은 시간순으로 가장 과거의 commit이다.)
- 일반적으로 하나로 합칠때 가장 위에있는 메세지를 pick으로 하고 아래있는 메세지들을 squash로 바꿔준다.
- pick과 s를 적절히 사용해주면 하나로 합쳐진 commit메세지를 다시 작성하는 터미널로 전환된다.
  - 이 때 주석 처리된 기존 커밋메세지들을 지우고 통합 커밋 메세지를 기존처럼 작성하면 된다.

#### git rebase를 취소하고 싶을 때
- `git rebase --rebort` : 그냥 리베이스전으로 되돌리는 방법
- `git reset --hard HEAD` : 오리진의 맨 꼭대기로 브랜치로 바꿔버림

### merge와 rebase의 차이
- merge : 커밋이 마스터위에 4개가 있을때 하나는 마스터 아래있는 경우 그대로 시간순서대로 합쳐진다.

- rebase : git pull하고 merge하는 것과같음 -> 커밋순대로 하나하나 차근차근 쌓는다는 느낌으로 마스터 위로 올라간다.


### rebase할 경우 에러사항 참고
#### 리베이스를 할 때 현재 branch가 최신인지 확인할 경우가 있다.
- 이유 : 커밋하고 푸쉬->커밋->푸쉬->피드백 이런식으로 계속 피드백받으면서 커밋메세지가 쌓일 경우에 리베이스하면 발생하는 에러이다.
```
 ! [rejected]        feature/user -> feature/user (non-fast-forward)
error: failed to push some refs to 'https://github.com/wecode-bootcamp/lunch-button-backend.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
이런식으로 거절메세지가 뜬다.

- 해결 : 같은 브랜치에서 풀을 받아온 후 다시 rebase해주고 `git push origin -f feature/user`를 해주면 된다.
  - -f 옵션은 강제로 푸시해주는 옵션이다.
  - 보통 같은 브랜치내에서 혼자 작업하는 경우는 괜찮지만, 혹시라도 같은 브랜치내에서 팀원이 작업하는 경우에는 서로 상의하여 결정하도록 하자.

### 그럼 임시 저장할 때 wip커밋 대신 stash를 써주면 안될까?
- stash  : 세이브는 하긴 싫고 다른 작업을 하고싶을때(갑자기 빔에러나 예상치못한 상황으로 모두 날려먹었을때 복구할수있다.)
  - stash는 보통 작업중인데, 다른 branch에서 작업을 하고와야할 경우에 사용한다.
  - stash를 할 때 add를 한 후 stash를 하면, stash pop을 할 때 다시 add해줘야한다.
- commit : 세이브할 준비가 됨 다만 완벽하게안되서 중간세이브를 해주는 것이다.

