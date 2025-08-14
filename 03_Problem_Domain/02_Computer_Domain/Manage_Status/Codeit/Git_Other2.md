## 깔끔한 커밋 히스토리를 원할 땐 git merge 대신 git rebase
git branch test
>new branch name test

git add .
git commit -m "Add get_Remainder function"

git checkout test
git add .
git commit -m "Add get_Remainder function"
...

git marge premium
conflic시 두개를 남김(HEAD와 test의 코드를 남김)

git rebase(베이스를 다시 지정하다=커밋을 재배치하다) test
> 현재위치한 프리미엄 브랜치의 베이스를 테스트 브랜치로 재지정
> 이부분도 충돌이 일어나면 수정해주면 된다.

다만 여기서 기존 merge키워드랑 차이가난다.
git rebase --continue : 컨플릭트가 발생해서 제대로 진행되지 못한 **리베이스를  계속 진행하라**
![[Pasted image 20250814183834.png]]
>원래 test가 프리미엄 브랜치에 있는거처럼 보인다.![[Pasted image 20250814183918.png]]
>![[Pasted image 20250814183930.png]]

## merge와 rebase차이
1. 리베이스는 새로운 커밋을 만들지 않는다.
2. 리베이스로 만들어진 커밋 히스토리는 머지로 만들어진 커밋 히스토리보다 더 깔끔하다.
3. 결과물은 서로 같다.

굳이 쓰는 이유는 커밋 히스토리를 깔끔하게 만들려고 **rebase**를 쓴다!
![[Pasted image 20250814184315.png]]