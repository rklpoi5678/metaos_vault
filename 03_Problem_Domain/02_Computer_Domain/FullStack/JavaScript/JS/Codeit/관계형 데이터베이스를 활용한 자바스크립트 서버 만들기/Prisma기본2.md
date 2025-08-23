## 마이그레이션
모델을 데이터베이스에 반영하는 과정을 마이그레이션이라고 한다.
스키마에 변경사항이 있다면 항상 마이그레이션을 해야한다.
```bash
npx primsa migrate dev
```

>가장 처음 마이그레이션 이름은 init을 많이지정합니다.(이러면 데이터베이스가 나의 스키마에 동기화되었다고 한다.)

실행시 새로운 파일이 migrations안에 있는데 이것은 내가 작성한 스키마문에 sql문으로 변경된 파일이다.(ORM -> SQL)

```bash
npx prisma studio
```
> 웹에서 해당 데이터베이스를 crud할수있다. gui처럼

## 테이블에 데이터가 있을 때 마이그레이션하기
```js
model User {

// .. 밑에 코드제외하고 원래코드
	age Int?
}
```
> prisma는 마지막 파일에 있었던 스키마를 기준으로 마이그레이션 파일을 만들고 실행한다. 그래서 해당 구조를 통해 무엇이 변했는지 알수있다는것이다.

> npx prisma studio를 하고 age 파일에 값을 채우고 ?(requerd를 지우든 말든)하고 지웠다면 다시 마이그래이션이 가능해진다.

```js
model User {
	// ...
	age Int
}
```
다만 필드를 지우는것은 현재 있는 데이터 열을 다지운다는 것이기에 그냥 코드를 지우고 마이그레이션 해도 작동하게된다.

primsa에서 마이그레이션 파일들은 데이터가 변화해온 과정들을 기록한다.(위에서 순서대로 정리되며 마이그레이션 파일들은 깃과비슷하게 지우지않는것을 추천한다.) 그래서 이것에 문제가 되거나 삭제되거나 변경사항이 있을경우 prisma에서 친절하게 메시지를 남겨준다.

## Prisma Client와 데이터베이스 CRUD 1

클라이언트에서 데이터를 가져올려면?
```js
import { PrismaClient } from '@prisma/client'

const primsa = new PriismaClient();
// 이런식으로 불러와서 사용하면된다.
// 이제 어떤 모델과 상호작용할려면 prisma.model.attr이렇게 쓰면된다.

app.get('/users/', async(req,res) => {
// prisma의 장점중 하나는 자동완성을 지원해준다는점이다. 또한 메소드에대한 정보들이 풍부하여 매우 유용하다.
// 해당 리턴값은 Promise이기에 await을 써줘야한다.
	const users = await prisma.user.findMany();
	res.send(users)
})
```
![[Pasted image 20250823214723.png]]```

```js
// 해당 아이디를 찾고싶을때(유니크값)
// findUnique메소드를 주면된다.
app.get('./users/:"id', async
 (req,res) => {
	const { id } = req.params;
	const user = await prisma.user.findUnique({
	//필터링 할껀데 아이디가 현재 아이디 인 에만 으로 필터링 하겠다.
		where: {id:id //그냥 id로 쓸수있다.}
	});
	res.send(user);
})
```

## Prisma Client와 데이터베이스 CRUD2
