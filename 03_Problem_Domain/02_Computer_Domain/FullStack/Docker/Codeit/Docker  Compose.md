## docker compose
여러가지의 컴포넌트를 쉽게 관리할수있게한다.
이떄 계층을 작성하는 파일을 yaml로 만든다.
```docker-compose.yaml
name: mbti
services:
  app:
    image: [계정명]/mbti:mysql
    build:
      args:
        - NODE_VERSION=20.15.1
      dockerfile: ./Dockerfile
      pull: true
      context: .
    container_name: app
    environment:
      - PORT=3000
      - DB_HOST=db
      - DB_PORT=3306
      - DB_NAME=db_mbti
      - DB_USERNAME=user_mbti
      - DB_PASSWORD=pw_mbti
    networks:
      - mbti-net
    ports:
      - 3001:3000
  db:
    image: mysql:8.3.0
    container_name: db
    environment:
      - MYSQL_ROOT_PASSWORD=root1234
      - MYSQL_DATABASE=db_mbti
      - MYSQL_USER=user_mbti
      - MYSQL_PASSWORD=pw_mbti
    networks:
      - mbti-net
    volumes:
      - mbti-vol:/var/lib/mysql
networks:
  mbti-net:
    name: mbti-net
volumes:
  mbti-vol:
    name: mbti-vol

```

## 서비스 간 의존 관계 설정하기
app은 db가 없으면 안되지만 db는  없어도됨 app->db는 의존한다(Depends On)
![[Pasted image 20250929001911.png]]
> 이런순서로 시작하고 종료해야  안전하다.

yaml에서 별다른 순서를 정해주지않으면 무작위로 실행한다.
```yaml
...
depends_on:
	- db
```
>  app이 의존하니 app 아래에다 해당  옵션을 넣어주자 즉, 서비스간의 실행순서를 제어할수있다.

유의점
엄연히 db 컨테이너와 app안 mysql서버가 잘구동되는것은 엄연히 다르다.
즉,  db컨테이너에 mysql서버가 정상적으로 실행이 안되더라도 app컨테이너가  실행되니  문제가있다는것.

이것을 해결할려면  condition, healthcheck등의 여러 세부사항을 지시해야한다.

depends_on 하나로만으로는 우리가 원하는 동작까지 이룰수는 없다는 점만 지금은 알면된다.