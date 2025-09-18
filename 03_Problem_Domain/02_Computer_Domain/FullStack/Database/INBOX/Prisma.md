## 핵심
데이터베이스와 코드 사이를 통역해 주는 도구이다. 우리의 말을 해석해서 필요한 책을 찾는것 Prisma는 그 해석기와 같다.

## 비유
거대한 도서관(DB) - 코드 - Prisma 도서관(DB)의 언어(SQL)로 바뀌주는 통역하이다. 

## 장점
안전장치 역활을 한다는 것이다. 타입스크립트와 같이 사용하면, 요청하는 데이터의 형태가 미리 정해져 있어 코드 작성 중에 실수를 예방할 수 있다.

### Database Seeding
테스트 데이터나 초기 데이터를 데이터베이스에 삽입하는 과정이다. 즉, 앱이 실행될때 필요한 기본 데이터를 미리 설정하는 것이다.

#### 예제
```Json
## package.json 에서 미리 설정한 예제
{
  "prisma": {
    "seed": "ts-node prisma/seed.ts"
  }
}
```
```Ts
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();

async function main() {
  await prisma.user.create({
    data: {
      name: "Alice",
      email: "alice@example.com",
    },
  });
}

main()
  .catch((e) => console.error(e))
  .finally(() => prisma.$disconnect());

```
- setting 실행 npx prisma db seed
- 위 명령어를 실행하면 seed.ts 파일이 실행되어 데이터베이스에 기본 데이터가 삽입된다.


### 첫 실행은 npx prisma init
데이터베이스 스키마 정보 연동을 위한 환경변수 설정에 필요한 .env 파일도 알아서 생성해준다.
또한 schema.prisma파일이 새로 생성됨

### prisma migrate dev
prisma db push는 데이터 손실 없이 스키마를 변경하는 방식 Prisma는 기존데이터가 있는 상태에서 필수(required)컬럼을 추가할 수 없기 때문에 오류를 발생시킴
현재처럼 필수 컬럼을 추가할 때는 prisma migrate dev를 사용하는 것이 더안전함
```Sh
npx prisma migrate dev --name add_user_id
```
이렇게 하면 마이그레이션 파일을 생성하여 안전하게 변경할 수 있음
기존 데이터를 삭제해도 괜찮다면, 데이터베이스를 초기화하고 변경 사항을 적용할수있다.
```Sh
npx prisma db push --force-reset
```
> 모든 데이터가 삭제되므로, 반드시 백업을 먼저 해야 한다.

### DEFAULT 값을 참조할수없음
PostgreSQL에서는 DEFAULT 값에 다른 컬럼을 참조할 수 없음
```Prisma
model User {
  id        Int    @id @default(autoincrement())
  username  String
  email     String @default(username) // ❌ 다른 컬럼 참조 불가능
}
```
Default 값은 고정된 값 또는 함수만 가능, 다른 컬럼을 참조할 수 없다.

### 잘못된 dbgenerated() 사용
degenerated()를 사용하여 기본값을 설정할 때, PostgreSQL에서 지원하지 않는 방식으로 적용했을 가능성이 있다.
```Prisma
model User {
  id String @id @default(dbgenerated("uuid"))
}
```
PostgreSQL에서는 uuid_generate_v4()같은 함수를 사용해야 함
```Prisma
model User {
  id String @id @default(dbgenerated("uuid_generate_v4()"))
}
```