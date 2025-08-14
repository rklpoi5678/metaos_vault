## git reset을 하고 나서 돌아올려면?
git reset --hard로 해도 커밋은 사실 사라지지않는다고 배웠는데 어떻게 다시되돌리나요?
reset을 해도 그 이후의 커밋들이 삭제되는 건 아니다.

git reset 도 다른 커밋으로 갈수있다고 배웠습니다.
git reset (과거 콘솔에서 가고싶은 커밋해시를 찾아입력)하면 다시 돌아간다.
단지 HEAD가 다른곳으로 가리키고있을뿐이다.

### **해시를 까먹었을때**
git reflog로 이때까지 HEAD가  가르킨 커밋을 출력한다.
다시 
git reset --hard 9856(or HEAD~x or HEAD^)![[Pasted image 20250814182323.png]]

## 현재 브랜치 말고 다른 브랜치까지 로그를 보고싶다면
git log --pretty=oneline
>현재 브랜치만보임

git log --pretty=oneline --all
> 메인브랜치와 프리미엄브랜치 로그가 둘다보입니다.
> 다만 혼동이 생길수있어서 --graph옵션을 줄수있다.
> --graph: 커밋 히스토리가 각 브랜치와의 관계가 잘 드러나도록 그래프 형식으로 출력

git log --pretty=on

