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