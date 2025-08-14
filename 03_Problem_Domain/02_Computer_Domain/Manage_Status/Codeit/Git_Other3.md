## 작업 내용 임시 저장하기
git stash(안전한 곳에 보관하다, 넣어두다): **working directory에서 작업하던 내용을 깃이 따로 보관(stack)** stack은 어떤 데이터를 저장하는 구조
> git stash : 현재 워킹 디렉토리를 스택으로 저장한다.

자료구조에서 스택이랑 똑같은데 동전쌓는것처럼 첫번째가 밑에 깔리면서 쌓이다가 맨위에서 하나씩 꺼내야한다.

git stash list : 스택에 저장된 stash내용을 리스트로 보여준다.
> 최근 커밋 이후로 작업했던 내용은 모두 스택에 옮겨지고, working directory내부는 다시 최근 커밋의 상태로 초기화

---

긴급한 작업을 처리하고 이제 다시 작업하던 내용으로 돌아간다.

---

## git stash apply(적용하다)
> 스택에 있는 내용을 다시 working direction로 가져와서 적용 
> 작업 했던 내용을 불러온다.

정리
git stash: 어떤 브랜치에서 하던 작업을 아직 커밋하지 않았는데 다른 브랜치로 가야하는 상황에서 **작업 중이던 내용을 잠깐 저장하고 싶을 때 사용한다.**

## 잘못된 브랜치에서 작업하고 있었다면? (git stash활용법)

git stash 
> 해당 브랜치가아닌 프리미움 브랜치에서 작업해야했다.!

git checkout premium

git stash list
> 혹시나 전에 저장되어있었던 스택이 있을수있으니 확실하게 불러와야겠다

git stash apply stash@{0}
> git stash list 에 나온 스테시 아이디를 넣어서 확실하게 불러온다.
> conflict 발생시 다시 에디터에서 수정

