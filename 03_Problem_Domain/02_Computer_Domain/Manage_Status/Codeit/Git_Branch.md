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
branch merge(병합하다, 합치다)

git marge main(master)
> 현재 위치인 (현재branch) 에 main branch를 합치겠다.
>  -m option이 없어 텍스트에디터가 나오는데

## 머지할때 conflict(충돌)
브랜치와 브랜치끼리 같은파일이네 내용이 다른경우 한쪽 브랜치에서 머지하는 상황에 충돌이 일어날수있다.
git marge main(master)
> CONFLICT (content) : Merge conflict in (충돌한 파일이름)
> 머지를 하다가 충돌이 발생했다!
> 둘중 어떤것을 반영해야하는지 깃에게 알려줘야한다.

```git
<<<<<<< HEAD //(현재 브랜치의 내용)
... 
=======
,,,
>>>>>>> master //(마스터 브랜치의 내용)

// 한부분을 지우거나(선택) 아니면 완전새로운 내용으로 변경시킬수있다. 
```
> confilct된 부분이 해결이되고 난뒤 다시 커밋하면 에디터에 Merge branch 'master' into (브랜치이름)가 자동으로 적혀있는데 확인하고 커밋

 정리
 1. 컨플릭트가 발생한 파일을 열고
 2. **머지의 결과가 되었으면 하는 모습**대로 코드를 수정한다.
 3. 커밋

### **다른 방법 아예 merge취소**


