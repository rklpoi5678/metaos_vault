## Pull Request를 위한 다양한 설정 및 편의 기능들

GitHub Repository설정 > Settings(보이지 않는다면 해당 레포지토리 권한이없는것 그런 경우 권한을 요처앻서 받으면 Repository Settings에 접근 가능)

일반설정 > Default Branch(일반적으로 main PR시 main에 머지됨, 때에 따라 develop으로 설정할수있으며 이러한 Default Branch를 변경하면 해당 브랜치로 머지를 요청하는 PR이 생성된다.)

**Pull Request의 머지 종류 제한하기**
머지하는 방법은 팀 내 정책에 따라 달라짐 이를 통일하고자 한다면 > ![[Pasted image 20250816232537.png]]
이 해당 이미지에 체크박스를 선택/해지 하는것으로 강제할수있다. 깔끔한 커밋 히스토리를 유지하고자 할 때 유용하게 사용될 수 있다.

### **PR가 머지된 이후, 자동으로 브랜치 삭제하기**
일반적으로 PR이 머지됐을 때 남아있는 브랜치들은 PR을 위해 생성한 일회성 브랜치이다, 이 설정을 선택하게 되면 PR이 머지됐을 때 자동으로 해당 브랜치를 삭제한다. 
> 불필요한 브랜치를 관리하는 수고를 덜 수 있다.![[Pasted image 20250816232945.png]]

### **브랜치 보호 설정**
개발자의 실수가 다른 개발자에게 영향을 미치는 것을 막아준다. 일반적으로는 main/develop등과 같이 여러 개발자들이 공유하는 브랜치에 보호 설정을 한다.
settings > Branches를 통해 설정 > Add branch protection rule 특정 브랜치들을 보호 상태로 설정할수있다.
![[Pasted image 20250816233110.png]]

### **Branch name pattern**
브랜치 보호는 브랜치의 이름을 기반으로 이뤄짐,(브랜치이름으로 보호설정을 걸수있음 main브랜치라면 main이라 적으면된다.)
또는 feature/* 와 같은 패턴을 사용한다면 > feature/abe || feature뒤에 오는 브랜치들이 룰을 적용받게된다.

### **Require a pull request before merging**(브랜치 보호룰 섹션안)
머지하기전 반드시 PR을 생성 하도록 설정한다. 해당 브랜치에는 직접 푸시하지 못하게 된다. 즉, 동료들의 리뷰를 받지 않고 main에 푸시하는 실수를 막을 수 있다.
![[Pasted image 20250816234614.png]]
> 위 이미지처럼 막힌다.

![[Pasted image 20250816234654.png]]
> 여기서 자주 사용하는 2가지 내용
> - Require approvals: PR이 병합되기 전 특정 수의 승인이 필요함을 명시가능(1명이면 1명이 승인하기 전까지 PR을 머지할수없음)
> - Require review from Code Owners: 특정 부분 책임을가진사람(Code owner)이 리뷰를 해야지 머지가 가능하도록 하는 설정


### **Require linear history**
PR을 통해 머지한 커밋이 선형적인 이력을 유지하도록 할 수 있다. 특정 브랜치에서 rebase나 squash방식만 사용하도록 강제하는 설정, 이설정을 활성화하고 머지하면 다음과 같은 화면이 나온다.
![[Pasted image 20250816234959.png]]

### **DO not allow bypassing the above settings**(경고로 끝나지않고 완전금지시킴)
경고만 해줄 뿐, 이 규칙을 반드시 따라야 하는건 아니다. > 떄문에 이 설정을 선택해야 어느 누구도 어길 수 없는 규칙으로 설정할 수 있다.

이 설정과 위에 다룬 Require linear history를 함께 선택하면, 아래 화면과 같이 머지 커밋을 만드는 버튼은 완전히 사용할 수 없게된다.
![[Pasted image 20250816235148.png]]
