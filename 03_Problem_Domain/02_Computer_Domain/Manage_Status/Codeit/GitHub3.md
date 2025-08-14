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

- --hard
- --soft
- --mixed

git reset을 하면 헤드가 과거의 커밋을 가리키게 할수있고(과거 커밋으로 아에돌아가고싶을때)
working directory의 내용도 과거 커밋의 모습으로 돌아가게 한다.

