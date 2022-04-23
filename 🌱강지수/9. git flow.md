## git branch 전략

- 여러개발자가 협업하는 환경에서 git 저장소를 효과적으로 활용하기 위한 work-flow
- 브랜치의 생성, 삭제, 병합이 자유로운 git의 유연한 구조를 활용하여 다양한 방식으로 소스 관리
- 브랜치전략이 있기 때문에 최신브랜치, 특정 기준 브랜치를 구분할 수 있음



### 자주 쓰이는 브랜치 전략

- git-flow
  - 5가지의 브랜치를 이용해 운영하는 전략
- github-flow
  - master브랜치와 Pull request를 활용한 전략



### git-flow

2개의 메인브랜치와 3개의 보조브랜치로 구성

- 메인 브랜치 : 항상 유지
  - master : 제품으로 출시될 수 있는 브랜치
  - develop : 다음 출시 버전을 개발하는 브랜치
- 보조 브랜치 : merge되면 사라짐
  - feature : 기능을 개발하는 브랜치
  - release : 이번 출시 버전을 준비하는 브랜치
  - hotfix : master 출시 버전에서 발생한 버그를 수정하는 브랜치

1. 개발자는 develop브랜치로부터 본인이 개발할 기능을 위한 feature브랜치를 만든다.
2. feature브랜치에서 오류가 발생한다면 release 브랜치 내에서 수정한다. QA가 끝났다면 버정늘 배포하기 위해 matser브랜치로 merge, bugfix가 있었다면 해당 내용을 반영하기위해 develop브랜치에도 merge
3. master에서 버그가 발생하면 hotfix 브랜치를 만들어 버그 수정이 끝나면  develop, master로 merge





![git flow](https://user-images.githubusercontent.com/43775108/125800526-2ea36d8e-6262-4ba5-9ef0-af7845131d85.png)  

git flow는 `feature`, `develop`, `release`, `hotfix`, `master`  5가지의 브랜치를 가진다. 

1. feature
   1. 기능의 구현을 담당한다
   2. `feature/{구현기능명}`
   3. develop브랜치에서 생성되어 develop브랜치로 머지된다
   4.  머지된 후에는 해당 브랜치를 삭제한다.
2. develop
   1. 개발을 진행하는 브랜치
   2. feature브랜치가 머지될 때 마다 develop 브랜치에 해당 기능이 더해진다.
   3. develop 브랜치가 배포수준이 되면 release 브랜치로 머지된다. 
3. release
   1. 개발된 내용을 배포하기 위해 준비하는 브랜치
   2. `release-1` 과 같은 방식
   3. release브랜치에서 충분한 테스트, 버그 검사 및 수정, 배포할 준비가 되면 master로 머지해 배포한다. 
   4. release브랜치는 develop브랜치에서 생성되며 버그 수정 내용을 develop브랜치에도 반영하고 최종적으로 master브랜치에 머지한다. 
4. hotfix
   1. 배포된 소스에서 버그가 발생하면 생성되는 브랜치이다. 
   2. `matster` 브랜치에서 생성되며 수정이 완료되면 develop, release, master에 모두 수정사항을 반영한다. 
5. master
   1. 최종적으로 배포되는 가장 중심의 브랜치
   2. develop브랜치에서는 개발이 진행되는 와중에도 이전 release내용이 master에 배포되어있다.



- 출처
  - 테코블 git 브랜치 전략 https://tecoble.techcourse.co.kr/post/2021-07-15-git-branch/

### git-flow특징

- 주기적으로 배포하는 서비스에 적합
- 가장 유명한 전략인 만큼 많은 IDE가 지원


### **Git** Flow

git 브랜치 전략중 git flow 전략과 비슷하게 upstream과 origin 저장소를 이용해 코드리뷰를 진행한다.  



**미션 방식**

```
master
- upstream공통저장소/master브랜치
- next-step/java-racingcar

develop
- upstream/id브랜치
- next-step/kang-jisu

feature
- origin/step1, local/step1브랜치
- kang-jisu/java-racingcar origin에서 step1,step2 브랜치를 생성하는것

origin은 fork한거, local은 컴퓨터에 받아온거 
```

- develop 브랜치에서 개발해야할 feature브랜치를 만든다.
  - upstream/본인id를 받아와 origin/step1을 만듦
- feature에서 만들다가 기능이 완성되면 develop에 merge
  - local/step1에서 만들다가 완성되면 origin/step1으로 push후 upstream/본인id로 pr요청
  - 리뷰를 마치면 upstream/본인id 브랜치로 merge
- master->main으로도 많이 명명  



### **git command**

**싱글 브랜치로 가져오기**

```bash
% git clone -b kang-jisu --single-branch https://github.com/kang-jisu/java-racingcar.git
```

`--single-branch` 를 사용하여 저장소에 모든 branch가 아닌 하나만 가져올 수 있다. 



**merge후 다음 단계 진행**

1. 브랜치 삭제 

```bash
git branch -D 브랜치이름 (강제삭제)
```



2. next-step/kang-jisu 즉 upstream(remote)의 develop브랜치가 merge되어 업데이트되었으니 그 최종 코드를 가져와야한다.

```bash
$ git remote add upstream https://github.com/next-step/java-racingcar.git

$ git branch -a
* kang-jisu
  remotes/origin/HEAD -> origin/kang-jisu
  remotes/origin/kang-jisu
  
$ git remote -v
origin  https://github.com/kang-jisu/java-racingcar.git (fetch)
origin  https://github.com/kang-jisu/java-racingcar.git (push)
upstream        https://github.com/next-step/java-racingcar.git (fetch)
upstream        https://github.com/next-step/java-racingcar.git (push)

$ git fetch upstream kang-jisu
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 1 (delta 0), pack-reused 0
오브젝트 묶음 푸는 중: 100% (1/1), 805 bytes | 805.00 KiB/s, 완료.
https://github.com/next-step/java-racingcar URL에서
 * branch            kang-jisu  -> FETCH_HEAD
 * [새로운 브랜치]   kang-jisu  -> upstream/kang-jisu
 
$ git branch -a
* kang-jisu
  remotes/origin/HEAD -> origin/kang-jisu
  remotes/origin/kang-jisu
  remotes/upstream/kang-jisu
```

- git remote add라는 명령어를 사용하여 remote를 바라볼 수 있도록 추가한다.
- git fetch를 이용해 upstream의 변경내용을 확인한다.



```bash
$ git rebase upstream/kang-jisu
Successfully rebased and updated refs/heads/kang-jisu.
```

- git rebase를 이용해 upstream/kang-jisu의 코드를 rebase한다. 
