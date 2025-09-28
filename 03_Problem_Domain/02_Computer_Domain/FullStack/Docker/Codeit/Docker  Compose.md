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
