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
mv는 똑같은 이름의 ㅍ