## Git의 핵심 구조와 파일의 상태관리
working directory에서는 실제 파일을 수정하며, 이 변경 사항을 다음 커밋에 반영하기 위해 Stage에 보관한다. `git commit` 명령어를 사용하면 staging area에 준비된 변경 사항이 repository로 이동하며, 새로운 버전이 생성된다.

파일 상태는 이과정에서 'Untracked','Modified','Staged','Unmodified' 등으로 변화하게 된다.

