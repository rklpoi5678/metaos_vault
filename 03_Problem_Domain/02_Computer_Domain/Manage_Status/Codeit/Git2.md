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
