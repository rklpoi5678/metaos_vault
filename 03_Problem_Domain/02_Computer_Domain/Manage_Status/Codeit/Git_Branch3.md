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
> merge시 위 이미지처럼 합병된다. (머지커밋)

## git reset의 비밀
![[Pasted image 20250814160215.png]]
>git reset \[--soft,--mixed,--hard]어떤 옵션을 쓰든
>1. HEAD는 여전히 같은 브랜치를 가리키고,
>2. HEAD가 가리키는 브랜치가 다른 특정 커밋을 가리키게 된다.
>3. 이 때문에 HEAD가 간접적으로 가리키던 커밋도 바뀌게 된다.

### **git reset을 한다고 그 이후의 커밋이 사라지는것이 아니다.**
그래서 git reset은 HEAD가 가리키는 커밋 이후의 커밋으로도 리셋할수있다.
위 이미지에서 git reset 43kf 하면 네번째 커밋으로 돌아가겠죠.

1. 과거의 커밋으로 git reset을 한다고 그 이후의 커밋들이 삭제되는 게 절대아니다.!
2. git reset은 과거의 커밋뿐만 아니라 현재 HEAD가 가리키는 커밋 이후의 커밋으로도 할 수 있다.

git checkout 9033
HEAD가 직접 커밋을 가리키는 말은 Detached(우리말로 ~로부터 떨어진,분리된) HEAD이다.
![[Pasted image 20250814161051.png]]
git branch premium
![[Pasted image 20250814161124.png]]
> premium브랜치는 HEAD가 가리키던 커밋을 똑같이 가리키게 된다.

! checkout 커맨드로는
- HEAD가 커밋을 직접적으로 가리키거나
- 브랜치를 직접 가리키게 할수있다.

git checkout premium
![[Pasted image 20250814161244.png]]
이 때 여기서 새로운 커밋을 하면 분기한다.

## 풀어쓰기
```git
git checkout master

= mv master
= HEAD -> master
= HEAD -> master - working directory내부도 그 커밋에 맞게 변함
= master에 온 사용자는 실감하게됨
```

### **git reset vs git checkout**
| git reset                            | git checkout                                         |
| ------------------------------------ | ---------------------------------------------------- |
| HEAD가 가리키던 브랜치가 다른 커밋을 가리키도록 한다      | HEAD 자체가 다른 커밋이나 브랜치를 가리키도록 한다                       |
| HEAD도 결국 간접적으로 다른 커밋을 가리키게되는 효과가 생긴다 | 브랜치를 통하지 않고, 커밋을 직접적으로 가리키는 HEAD를 Detached HEAD라고 한다 |