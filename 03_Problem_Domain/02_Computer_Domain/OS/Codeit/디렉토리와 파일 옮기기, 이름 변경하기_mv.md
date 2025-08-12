## 핵심
mv path1 path2

path1: 작업할 대상의 경로
path2: 이동할 목적지 또는 변경할 이름

path2에 아무것도 없다면 디렉토리가 생성되고
있다면 이름이 변경됩니다.

```bash
mv Jul Aug
Aug라는 디렉토리가 없다변 이름이 바뀌고
있다면 Jul이 Aug디렉토리 안으로 이동합니다.

mv Aug/Jul .
다시 안에 Jul을 현재 디렉토리로 옮기는 명령어 입니다.

mv finances.txt Sep
finances.txt파일이 존재하기때문에 Sep안으로 들어갑니다.
```

> 즉, path2가 실제로 존재하느냐 아니냐 없다면 이름이 바뀌고 있다면 해당 디렉토리안으로 옮겨질것이다.

## 주의점
mv는 똑같은 이름의 파일을 덮어버릴수있다는것이다.
```bash
현재 폴더안 test1.txt test2.txt 존재
mv test1.txt test2.txt를 한다면? 
> test1.txt이 파일내용이 test2.txt에 들어가면서 이름을 test2.txt로 변경시키게된다. 즉 덮어쓰기가 된다.
```
이런 현상을 방지하고 싶다면 i(interactive)를 쓴다.
> 만약 충돌이있다면 사용자에게 어떻게 할것인지를 물어봅니다.

```shell
mv -i test1.txt test2.txt
.
.
.
overwrite test2.txt(y/n [n]) n
```
> 안전하게 mv명령어를 사용하고 싶다면 -i 옵션을 사용하셔라

