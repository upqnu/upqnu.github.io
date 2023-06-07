---
layout: single
title: "Git - Merge와 Rebase는 둘 다 잘 써야 한다!"
categories: Git&Github
tag: [merge, rebase, git graph]
---

### [Git - Merge와 Rebase는 둘 다 잘 써야 한다!]  
  
Git flow를 사용하든, github flow를 사용하든, 나름대로 변형시켜서 사용하든 ~ 기본적으로 먼저 merge와 rebase를 적절히 사용할 수 있어야 한다. 그래야 브랜치를 심플하고 깔끔하게 유지할 수 있기 때문이다.
  
일단 merge와 rebase를 비교해보자.
  
- merge (병합) : 두 브랜치를 한 커밋에 이어 붙임. 합쳐진 브랜치의 사용 내역이 남는다. 아래 예시는 pjt 브랜치를 main 브랜치로 merge하는 것을 가정함
    1. `git switch main` : 반드시 merge 후 남겨질 브랜치명(여기에서는 main)으로 이동해야 함 
    2. `git merge pjt` : merge (병합)
    3. `git branch -d pjt` : merge 이후 합쳐진 prj 브랜치를 삭제
    - Merge도 commit이다! 잊지 마시길!
  
- rebase (재배치) : 브랜치를 다른 브랜치에 이어 붙임. 합쳐진 브랜치의 사용 내역은 사라진다. 아래 예시는 cdp 브랜치를 main 브랜치로 rebase하는 것을 가정함 (아래 순서를 꼭 지킬 것)
    1. `git switch cdp` : (merge와는 반대로) rebase의 대상이 되는 브랜치명(여기에서는 cdp)으로 이동해야 함
    2. `git rebase main` : rebase (재배치)
    3. 소스트리 등에서 확인하면 main이 cdp보다 뒤쳐져 있음. 그래서 main을 cdp의 시점으로 fast-forward하기 위해
    4. `git switch main` : 우선 main으로 이동 후
    5. `git merge cdp` : cdp를 merge한다
    6. `git branch -d cdp` : merge 했으니까 합쳐진 cdp 브랜치를 삭제
    - 협업 시, 팀원과 공유된 commit에 대해서는 사용하지 않는다
  
※ switch 대신 checkout을 써도 무방하다.  
  
=====

깔끔하게 정리한 것 같지만, 명령어를 이해하고 외웠다고 개념까지 잘 들어오지는 않는다. 다음 예시를 통해 merge, rebase 차이를 설명해보겠다.

<img width="918" alt="image" src="https://github.com/upqnu/upqnu.github.io/assets/101033614/16fda846-f09d-4a68-a844-1ffede20ab3c">  
  
main 브랜치에서 3번의 커밋 후, 2개의 브랜치(feat1, feat2)를 분기하였다. 그런데...  
  
  
<img width="1009" alt="image" src="https://github.com/upqnu/upqnu.github.io/assets/101033614/a8b2118d-be8d-454b-a538-63b229b65871">
  
갑자기 feat1이 main에 merge되었다. 이 경우, 2가지를 선택할 수 있을 것이다.  

(1)
<img width="1186" alt="image" src="https://github.com/upqnu/upqnu.github.io/assets/101033614/3cee8941-d12c-4a12-8e03-0350815904a7">
  
첫번째는 feat2 또한 main에 merge하는 것이다. 하지만 이러면 그래프는 복잡해진다. 만약 git flow를 사용하는데 dev, release(QA), hotfix 등의 브랜치를 이렇게 merge만 해댄다면?  
그래프는 보기 싫어지고, 브랜치 여러 곳에서 복잡한 conflict들이 생겨날 것이며, 서비스에는 오류가 속출할 것이다.  
  
  
(2)  
<img width="1346" alt="image" src="https://github.com/upqnu/upqnu.github.io/assets/101033614/4135383e-98f2-40ce-97bf-587b693de7ec">  
  
git rebase는 현재 checkout된 브랜치에서 자신의 부모 커밋(베이스)를 변경할 때 사용한다. 설명하고 있는 이 케이스에서 feat2의 부모 커밋은 'commit3'이다. 그런데 rebase 사용하여 feat2 브랜치 잘라서 main에 붙이면 -> main의 최신 커밋인 'Merge feat1'을 새로운 부모로 삼아 깔끔하게 잘 올라간 것을 볼 수 있다.  
"feat2가 어디로 사라진 거야?"라고 궁금해하지 말자. rebase는 합쳐진 브랜치의 사용내역이 사라지니까.  
  
=====

여기까지가 끝인가 보오~하면 안 된다. rebase의 깔끔함은 merge로 마무리해야 비로소 완성되기 때문이다. main으로 이동해서 feat2를 merge한 후, feat2 브랜치까지 삭제해야 이 험난한(?) 과정은 마무리 된다. 그러면  
<img width="851" alt="image" src="https://github.com/upqnu/upqnu.github.io/assets/101033614/e971e39e-0d34-4ce7-8ab9-05c6649fc0ad">  
  
브랜치가 2줄로 깔끔하게 유지되는 심플함을 눈으로 확인하게 된다.  
  
=====
  
### [인텔리제이에서도 Git Graph 비슷한 걸 쉽게 띄울 수 있다.]  
  
IDE로 VScode를 사용하면 "Git Graph"를 사용하여 깃 브랜치들을 눈으로 쉽게 확인할 수 있다. 그런데 Intelli J에서도 쉽게 확인할 방법이 없을까 찾아보다가 역시나 쉽게 확인할 방법을 있음을 찾았다.  
  
<img width="1058" alt="image" src="https://github.com/upqnu/upqnu.github.io/assets/101033614/7f633c38-f739-49f9-859f-3f9d7213cdce">  
  
  
맥북 기준 ; View > Tool Windows > Git을 클릭하면  
  
![image](https://github.com/upqnu/upqnu.github.io/assets/101033614/adbbf806-f4c1-4ce4-89f2-0990faa2aac5)  
  
위 캡처와 같이 브랜치 및 커밋 내역 등을 비주얼하게 확인할 수 있다. (다른 사람들 인텔리제이에선 더 컬러풀했는데 왜 내껀...ㅠㅠ)  
  
   
▶︎ 포스팅 작성을 위해 참고한 정보는 다음과 같습니다 ~ :

https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-Rebase-%ED%95%98%EA%B8%B0

https://upsw-p.tistory.com/41  

https://wbluke.tistory.com/26  

얄팍한 코딩사전 - 제대로 파는 Git & GitHub - 깃 끝장내기(https://www.youtube.com/watch?v=1I3hMwQU6GU)  

  