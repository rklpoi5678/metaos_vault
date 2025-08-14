## 두 커밋 간 차이 보기
git histiory(이전 alias)

git diff(difference,차이점) (그 이전의 커밋해시) (그 이후 커밋해시)
>git diff facd eea5
>git show커맨드 처럼 나오니 git show에서 보았던것처럼 읽으면된다.

## HEAD
.git 디렉토리안에 파일에도 있으며, 어떤 커밋 하나를 가리킨다.
> 보통 가장 최근에 한 커밋을 가리킨다.
> 매번 자동으로 더 새로운 커밋을 가리킨다.

working directory/working tree는 HEAD가 가리키는 커밋에 따라 구성
HEAD가 다른 커밋을 가르키면 working directory는 언제든지 바뀔수있다. 

### **이전 커밋으로 git reset하기**
git reset --hard (가고싶은 커밋의 아이디값)
> 다시 로그를찍어보면 달라진다.
> hard옵션을 썻기때문에 워킹 디렉토리 내부도 바뀐다.

아래는 깃의 3영역중 몇개까지 리셋을 하는냐를 가리키는 옵션이다.
- --soft: 레포지의 헤드가 (ea5)커밋을 가리킨다. 워킹 + 스테이징공간 안바뀜
- --mixed: 레포지의 헤드가 (ea5)커밋을 가리킨다. 스테이징공간이 바뀜
	- 작업한 작업이 남아있지만 스테이징공간은 해당커밋아이디로 바뀜
- --hard:  레포지의 헤드가 (ea5)커밋을 가리킨다. 둘다 바뀜
	- 커밋 이후로 한 작업이 전부 사라집니다. (비권장, 복구가안됨)
	- 의도한것이면 상관없고, 원격 레포지토리가 있었다면 다시 git pull로 복구가 가능합니다.

git reset을 하면 헤드가 과거의 커밋을 가리키게 할수있고(과거 커밋으로 아에돌아가고싶을때)
working directory의 내용도 과거 커밋의 모습으로 돌아가게 한다.

staging area에 넣고 커밋해도 이 공간을 초기화되지않는다. 계속 git add할 때마다 staging area에서는 새로운 파일이 추가되거나 원래 있던 파일이 더 새로운 버전의 것으로 교체되거나 할뿐이다.

## HEAD를 기준으로 git reset하기
git reset --hard HEAD^
>HEAD^은 현재 HEAD가 기리키고 있는 **커밋의 바로 이전 커밋을 나타낸다**.

git reset --hard HEAD~2
>HEAD~2는 현재 HEAD가 가리키는 커밋보다 **2단계 전에 있는 커밋(전 전)** 을 나타낸다.

