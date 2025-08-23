## Prisma 초기화
npx prisma init --datasource-provider postgresql
> npx -> nodePackpageExecuter

```.env
DATABASE_URL="postgresql://johndoe:rnadompassword@localhost:5432/mydb?sdchema=public"
PORT:3000
```
> window: gostgres:password
> mac: username:password
> localhost다음에나오는 mydb쪽은 해당 이름이 데이터베이스에 없다면 생성해줍니다.

### **schema.prisma**
데이터베이스 모델을 설정하는부분
```prisma
# 사용할 클라이언트관련 설정
generator client {
	provider = "prima-client-js"
}

# 사용할 db 설정
datasource db {
	provider = "postgresql"
	url      = env("DATABASE_URL")
}
```

## User 모델 만들기

! 보기 좋게 자동 포맷팅을 시킬려면 
윈도우: Shift + Alt + F
mac: Shift + Option + F
linux: Ctrl + Shift + I
```prisma
# 적어도 하나의 유니크가 필요하다.
# @id는 User모델을 식별하는 아이디
@ 기본적으로 id는 db에서 관리하는 경우가 많다. @default로 db에 관리하게한다.
# uuid는 36자로 이루어진 아이디형식이다.

# Int @id default(autoIncrement())를 사용하면 숫자가 하나씩증가하는 아이디를 만들수있습니다.

# @unique는 유니크 어트리뷰트
# 필드는 값이 기본적으로 required이다.
# ?는 기본적으로 null 필수가아니다.
model User {
	id String @id @default(uuid())
	email String @unique
	firstName String
	lastName String
	address String
	
#저장된 시점을 디폴트(지금시간)으로 설정
	createdAt DateTime @default(now());
#업데이트 타입은 그냥 어트리뷰트로 updatedAt을 주면된다.
	updatedAt DateTime @updatedAt	
}
```
> 필드이름 | 필드타입 | 어트리뷰트

## Prisma Schema 추가 기능
`enum`
유저의 멤버십 타입을 지정한다고 치자,
멤버쉽은 BASIC과 PREMIUM 2가지 타입이 있는데 이렇게 필드의 값이 몇 가지 정해진 값 중 하나일 때는 enum(enumerated type)을 사용할수있다
```js
model User {
	// ...
	membership Membership @default(BASIC)
}

enum Membership {
	BASIC
	PREMIUM
}
```
이넘값은 대문자
필드의 타입을 이넘이름으로 지정
> SQLite에서는 이넘을 사용할수없다.

`@@unique`
여러 필드의 조합이 유니크해야하는경우
@@unique어트리뷰트 사용
특정 필드에 종속된 어트리뷰트가 아니기 때문에 모델아래에 씁니다.
```js
model User {
	id String @id @default(uuid())
	email String @unique
	firstName String
	lastName String
	address String
	createdAt DateTime @default(new())
	updatedAt DateTime @updatedAt
	
	// 두 조합이 유니크가 되게설정
	@@unique([firsName, lastName])
}
```
-->
```json
// 삽입 가능
{
	id: "abd",
	firstName: "길종",
	lastName: "홍",
	// ...
},
{
	id: "def",
	firstName: "길종",
	lastName: "박",
	// ...
}
// 삽입 불가능
{
	id: "abd",
	firstName: "길종",
	lastName: "홍",
	// ...
},
{
	id: "def",
	firstName: "길종",
	lastName: "홍",
	// ...
}
```
