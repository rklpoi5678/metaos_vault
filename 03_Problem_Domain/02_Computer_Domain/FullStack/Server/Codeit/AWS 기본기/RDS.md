또 하나의 특별한 기능을 제공하는데 ,  AWS에서 제공하는 데이터베이스이다.
 Relational Database Sevice(RDS는 관계형  데이터베이스이다.)
 EC2에 안에 db를 설치해서 사용하는게 더  경제적일수있다. RDS에 나가는 비용이 더크기때문이다.
 다만 EC2에서쓰면 시스템업데이트,데이터백업, 필요에 따른 확장/축소, 장애 해결 등 생각할내용이 많아진다.

##  SSH터널링
RDS안에 데이터베이스를  여러개만들수있다.(여타 다른 디비랑 똑같음)
VPC안에 퍼블릭과 프라이빗IP (EC2와 VPC관계와 똑같다.)
![[Pasted image 20251004024527.png]]
> 이런방식을 SSH 터널링 이라고도 한다.

## DB 인스턴스 생성하기
엔진 옵션(MySQL기준으로 하겠습니다.) > DB  인스턴스 식별자 이름 설정 >  비번등 설정 > 인스턴스 구성  > 스토리지 설정  > EC2 컴퓨팅  리소스에 연결 > 있는 EC2 인스턴스 클릭  > 퍼블릭엑세스는 가격을  생각하고  설정 > 백업(해두는게 좋은데 그만큼 저장용량이 늘어나 비용생각) 

보안 > 인바운드 규칙(밖에서 안으로  들어것을 허용할지 말지 규칙) >  아웃 바운드 규칙도 확인해본다.

##  DB 인스턴스 연결하기
mysql workbench 있으면 좋겠죠
connection Name  setting >  Standard TCP/IP over SSH(SSH을 이용할것이니) >  SSH Hostname, SSH Username, 패스워드입력, SSH key file(발급받은 키를 불러온다.), MySQL Hostname (RDS에 엔드포인트를 넣어준다.) 포트, 유저네임, 페스워드입력 >경고창이 나오면 잘연결되었음
```sql
show  database;
```

## SQL로 하는 DB작업
```sql
CREATE DATABASE shop
SHOW databases;

---

USE shop

---
CREATE TABLE customer (
	id  INT,
	name VARCHAR(255),
	email VARCHAR(255),
	PRIMARY KEY (id)
);
SHOW table
---
INSERT INTO customer (id, name, email)
VALUES
	(1, 'Alice', 'alice@example.com'),
	(2, 'Bob', 'bob@example.com'),
	(3, 'Charlie', 'charlie@example.com');
---
SELECT * FROM customer
```
## ORM
@aws-sdk/client-rds: 세부 조작 보다는 전반적인 관리에 주로 활용
orm( object relational mapping)
-  단점:  js -> sql언어로 번역될때 시간이 걸릴수도있다.
Sequelize라는 ORM을 사용해보겠다.