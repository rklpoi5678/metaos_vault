## 핵심
나무가지 처럼 뻗어나가는것을 브랜치라고한다.
깃은 루트 커밋을 기준으로 가지처럼 뻣어나간다.![[Pasted image 20250814144319.png]]

git status
> On branch main(master): 메인 브랜치 위에있다는 말이다.
> 메인은 레포지토리를 만들고 커밋을 하면 자동으로 생기는 브랜치다.
> 기본 브랜치

git branch (만들고싶은 브랜치 이름)
> 이때 까지 한작업들도 모두 해당 브랜치 이름에도 들어가게 된다.

git checkout (가고싶은 브랜치 이름)
> 이제 여기서 작업하고 커밋하면 main브랜치와는 상관이없게된다.

git branch
> 이때 까지 만들어둔 branch이름들이 보인다.

git branch -d (브랜치 이름)

git checkout -b(branch) (만드고싶은 브랜치 이름)
> branch를 만들고 체크아웃한다.

## 브랜치 merge하기

