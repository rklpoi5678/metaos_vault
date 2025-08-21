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

{

timeseries: true,

}

);

  

// model dms scheam rlqksdmfh whghl,update,delete interface

// first argument firstLetter.upperCase + Single -> MongoDB Collection Name

const Task = mongoose.model('Task', TaskSchema);

  

export default Task;
```