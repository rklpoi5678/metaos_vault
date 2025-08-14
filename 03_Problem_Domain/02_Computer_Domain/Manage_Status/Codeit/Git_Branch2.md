## 핵심
origin이란?
> git remote add origin http://github.com/.../...

remote는 리모트 레포지토리관한 작업을 할 때 쓰는 커맨드
add는 새로운 리모트 레포지를 등록하겠다.
origin: 주소.git 리모트 레포지토리를 **origin**이라는 이름으로 등록하겠다.

## 왜 origin이라고할까?
관례화가 되어있기때문 (근원,기원 = 프로젝트의 근원이 되는 존재이기에)
Git에서 리모트 레포지토리를 최초로 추가할 때 오리진이라는 이름으로 가리키게 관례화가 되어있다.
>사실 git remote add hello ... 사용해도문제는없는데 관례에 따라 origin 으로 써준다.

## Remote Repositoy에 있는 브랜치
git push -u origin master
>로컬 레포지에있는 모든 master 브랜치의 내용을(=main 브랜치와 관계된 모든 커밋들)
>origin이라는 리모트 레포지토리로 보낸다는 뜻이다.

만약 origin에 master 브랜치가 없다면 마스터 브랜치를 새로 생성하고 푸시한다.

옵션 -u
- --set-upstream이라는 옵션의 약자이다.
- 로컬 레포지에 있는 마스터 브랜치가
- 