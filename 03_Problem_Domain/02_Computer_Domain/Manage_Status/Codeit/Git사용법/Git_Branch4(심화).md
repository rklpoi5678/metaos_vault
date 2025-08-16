## 새로운 커밋을 만들지 않는 머지도 있습니다.

![[Pasted image 20250814161811.png]]git merge premiom![[Pasted image 20250814161829.png]]
새로운 커밋이 생기는 게 아니라 단지 브랜치가 이동하게 되는 머지를 **Fast-forward머지**라고 한다. 빨리감기 한다는말인다. 지금 마스터브랜치가 더 최신 커밋으로 이동하는모습과 비슷하다.
> 같은 선상 브랜치를 머지할때 Fast-forward머지가 이루어진다.
![[Pasted image 20250814162017.png]]
분리된 2개선상에서 머지 커밋을 하면 새롭게 커밋이 생긴다.(=3-way merge)
**이름이 3-way인 이유는 지금 1,2,3 표시한 3가지 커밋을 고려해서 머지를 하기 때문이다.**
- 1번 두갈래로 갈라지기 전 공통 조상이 되는커밋
- 2번 한 브랜치가 가리키는 커밋
- 3번 다른 브랜치가 가리키는 커밋
-> 3-way merge는 자신만의 방식을 갖고 이 3가지 커밋을 기준으로 머지 커밋을 자동으로 만들어낸다.

## 3-way merge

base a master a premium b = B
3-way merge는 base에서 변화가 발생한 것을 우선 채택합니다. 그래서 머지 결과 'B'가 된다.

base 1 master 2 premium 1 
base에서 변화가 발생한 2가 머지 결과가 된다.

base "hello" master "" premium "hello" = 공백 상태가 된것이기에 변화가 더 발생한것이기 때문에 머지 결과는 공백이된다. 

base "bye" master "fighting" premium "please"
두 브랜치 에서 다 변화가 있을 때 Git은 어떤 변화를 선택하냐면 모른다를 선택한다
-> conflict 발생

