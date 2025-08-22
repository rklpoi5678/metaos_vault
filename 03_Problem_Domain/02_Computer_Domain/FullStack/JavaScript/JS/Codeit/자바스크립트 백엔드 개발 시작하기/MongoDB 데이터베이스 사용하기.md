## MongoDB
- 로컬
- 클라우드(원격): MongoDB Atlas라는 클라우드 서비스를 제공한다.

## Mongoose
experss안 db연결 -> 라이브러리 사용
```bash
# Mongoose는 자바스크랍트를 사용해서 MongoDB 데이터베이스와 소통할 수 있게 해주는 라이브러리이다. Mongoose가 제공하는 API를 이용해서 데이터베이스에 접속하고 CRUD(Create, Read,Update,Delete)d연산을 하는것
npm i mongoose@"<8.0.0"
```

```js
import mongoose from 'mongoose';
import { DATABASE_URL } from './env.js';

// ...

mongoose.connect(DATABASE_URL).then(() => console.log('Connect to DB'))
```
`mongoose.connect()` 메소드에 `DATABASE_URL`을 전달해서 데이터베이스에 접속하는 겁니다. 이작업은 비동기로 이루어지며 `.then()`메소드활용시 `Connected to DB`라는 메시지 출력

##

```js
import mongoose from 'mongoose';

const TaskSchema = new mongoose.Schema(
	{
		title: {
			type: String,
		},
		description: {
			type: String,
		},
		isComplete: {
			type: Boolean,
			default: false
		},
	},
	
	// mongoose auto createAt,updateAt
	// 몽구스는 자동으로 스키마 두번째에 해당 옵션을 주면 create,update관리해줌
	{
		timestamps: true,
	}
);

// model은 scheam기반으로 조회,업데이트,삭제하는 인터페이스
// 첫번째 아큐먼트는 대문자로 시작+ 단수형으로 작성하며
// 이것은 몽고디비에 컬렉션 이름에 영향을 줍니다.
const Task = mongoose.model('Task', TaskSchema);

export default Task;
```

## 시드 데이터 넣기
초기데이터를 넣는과정을 시딩, 초기 데이터를 시드데이터라고 한다.
> mockdata는 일반적인 초기데이터나 테스트데이터를  말하는거고,
> 시드데이터는 데이터베이스에 쓰는 초기데이터를 말함

```js
//mock.js에 id는 몽고디비에서 자동으로 생성하기 떄문에 id는지운다.
//seed.js

import mongoose from 'mongoose';
import data from './mock.js';
import Task from '../models/Task.js';
import { DATABASE_URL } from '../env.js';

// 이 파일은(env.js)는 DB를 초기데이터로 리셋하는 역할
mongoose.connect(DATABASE_URL)

// 비동기를 받기 때문에 await을 써줘야한다는점
await Task.deleteMany({}); // 삭제조건을 파라미터로 받음, 빈객체 => 모든 조건만족 전부삭제
await Task.insertMany(data); // 삽입할 데이터를 파라미터로 받음

mongoose.connection.close(); // 종료시킨다.
```
```json
#이제 시드라는 명령 스크립트를 넣어준다.
"scripts": {
	...
	"seed": "node data/seed.js"
}
```
> npm run seed하면 atlas에 성공적으로 시딩한 데이터 시드데이터가 들어왔다
> __v는 몽고디비에서 내부적으로 사용하는값이기에 무시해도된다.

## 데이터 조회하기
```js
// 파일변수 이름클릭후 f2를 누르면 전체 이름을 변경시킬수있다.
import mockTasks from './data/mock.js';
import Task from './models/Task.js';

// await 사용시 함수에는 async
app.get('/tasks/:id', async (req,res) => {
	// 몽고DB는 기본적으로 아이디부분은 문자열을 받음
	const id = req.params.id;
	// findById라는 메소드 제공
	const task = await Task.findById(id);

})

```