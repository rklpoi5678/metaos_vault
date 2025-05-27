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
