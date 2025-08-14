##  HEAD와 branch관계
헤드는 어떤 커밋 하나를 가리키고
브랜치는 하나의 코드 관리 흐름을 나타낸다.

-> 어떤 커밋을 가리키는 존재 -> 포인터

HEAD는 (working directory)commit을 직접적으로 가리키지않는다. branch를 가리킬뿐이다.![[Pasted image 20250814154827.png]]
git checkout premiom을 하면 헤드는 premium브랜치를 가리키게된다. 이상태로 커밋을 하면 아래그림처럼된다.
![[Pasted image 20250814154943.png]]
여기서 마스터로 간다음 다시 커밋을 하면 분기점이 생기면서 갈라집니다.(=분기한다.)
![[Pasted image 20250814155032.png]]
![[Pasted image 20250814160033.png]]
> merge시 위 이미지처럼 