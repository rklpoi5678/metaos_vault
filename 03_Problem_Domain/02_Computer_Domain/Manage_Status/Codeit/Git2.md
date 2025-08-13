## 핵심
git status : 현재 깃의 변경사항을 말함
- Changes to be committed - 커밋에 반영될 변경사항 (1)
- Changes not staged for commit - 커밋에 반영되지 않는 변경사항 (2)
즉 커밋을 하면 1번이 저장소에 저장되고 2번은 변경되지않고 저장된다는말이다.

디렉토리를 git add하면 안에있는 파일들도 1번 변경사항으로 올라간다.(stage에 올라간다.)
모든 변경사항을 모두 스테이징으로 올릴려면 
`git add .` : 현재 프로젝트 디렉토리 내에서 변경사항이 생긴 모든 파일들을 staging area에 추가하라
> 위처럼 git add . 으로 쓸때가 많습니다.

## Git이 보는 파일의 4가지 상태
git으로 관리되는 파일은 일종의 상태(status)를 가진다는 사실
크게 2가지
- Untracked status: 추적이 안되고있다. git add를 한번도 안했을때
- Tracked status : 추적이되고 있는 상태 특징에 따라 3가지로 또 나뉨
	- Staged status: staging area에 올라가있음
	- Unmodified status: 최신 커밋과 변경사항이 없을때 추가로 커밋이후에 는 working directroy안의 모든 파일들이 이 상태가된다.
	- Modified status: 조금이라도 바뀐 내용이 있는 상태면 그 파일은 Modified(수정된) 상태이다.
	- git 파일은 매순간 4가지 상태 중 하나의 상태에있는다.
![[Pasted image 20250814003650.png]]
> 파일을 삭제하면 당연히 Git에서 더이상 인식하지않는다.


## git add 취소하기 (git reset)
git reset (여기에 해당 파일/디렉토리 이름): staging area에서 파일 제거
즉 stating area에서 내리는것이다.
>reset을 해도 삭제되는것이 아닌 working directory에 있다.

수정시 전과 같다면 nothing to commit, working tree clean이 뜰것이다. 즉, 전과 같아서 차이가 없으니 Unmodified상태가 되는것
clean: 이전 커밋 이후로 변경사항 없음!

## 특정 git 커맨드의 사용법
git help (알고싶은 커맨드 입력) or man git-(알고싶은 커맨드)
둘다 같은 결과를 출력한다.
해당 결과에서 나가고 싶을땐 q(quit)입력