## 데이터 생성과 유효성 검사
데이터 생성은 
await Task.create(req.body)
res.status(201).send(newTask);

데이터 유효성 검사는 사용자가 전달하는데이터가 올바른지 확인하는과정이다.
몽구스는 scheam로 추가할수있다.
```js
// 필수 required로 maxLength로 받을수있는 최대길이 설정
// 최대 길이를 초과하면 ValidationErrro가 나온다.
// 몽구스는 스키마에 정의되지 않은 필드는 무시한다.
{
	title: {
		type: String,
		required: true,
		maxLength: 30,
		//validator를 만들어 2단어가 이상이어야 되게만들기
		validate: {
			validator: function(title) {
				return title.split(' ').length > 1;
			},
			message: 'Must contain at least 2 words.',
		},
	},
}
```
문자열 길이는 : `minLength/maxLength`
속성,숫자 값은: `min/max`
문자열이 특정 값 중 하나인지는 `enum`
```json
{
	title: {
		type: String,
		maxLength: 20,
		required: true
	},
	price: {
		type: Number,
		required: true,
		min: 0
	},
	cycle: {
		type: String,
		required: true,
		enum: ['x','y']	
	},
	firstPaymentDate: {
		type: String,
		required: true
	}
}
```
20이상문자열필수, 넘버형 숫자 0이상 필수, x,y둘중에 하나 필수필드, 필수필드
```js
app.post('/subscriptions', async(req,res) => {
	const newSub = await SubscriptionModel.create(req,body);
	res.status(201).send(newSub);
});
```

## 비동기 코드 오류 처리하가
가장 직관적인것은 모든 await문을 try-catch로 잡는것
-> 효율적이지 않아 그러한 함수를 만드는것이다.
```js
// 추가적으로 오류는 잡는 함수이다.
function asyncHandler(handler) { //라우터로 들어가는 param을 파라미터를 받아 
	// 또다른 핸들러함수를 리턴
	// 추가적으로 오류처리가 되는 함수이다.
	// async의 파라미터는 함수라는것!
	return async function(req,res) {
		try {
			await handler(req,res) // 원래 있던 핸들러를 실행하고
		} catch (e) {
			console.log(e.name); // 오류가 발생하면 네임,메세지 프로퍼티를 출력
			console.log(e.message);	
		}
	}
}
```
```js
// 이제 추가적으로 비동기 코드에서 오류 처리를 함수를 이용해서 구현하였다.
app.post('/tasks', asyncHandler(req,res) => {
	const newTask = await Task.create(req.body);
	res.status(201).send(newTask);
})
```
> 이제 서버가 죽지않고 오류이름과 오류메시지를 출력할것이다.
```js
//이제 catch문을 수정
// 사용자 측인지 서버측인지 판단을 할수있다.
		} catch (e) {
			if(e.name === 'ValidationError'){
				// 400: 사용자 측에서 잘못보낸다.
				res.status(400).send({ message: e.message })
			} else if (e.name === 'CastError'){
				res.status(404).send({ message: 'Cannot find given id.'})
			} else {
				// 그외의 경우는 모두 500을 리턴
				// 서버측에서 무언가가 잘못되었다!
				res.status(500).send({ message: e.message })
			}
		}
```
```js
// 이런식으로 asyncReqHandler 를 리턴하는방법도 있다.
function asyncHandler(handler) {
  async function asyncReqHandler(req, res) {}

  return asyncReqHandler;
}
```

## 데이터 수정하고 삭제하기
특정 아이디에 있는 데이터를 삭제할때
`findByIdAndDelete(아이디)`를 사용할수있습니다.

## 정리
**스키마와 모델**: schema는 데이터의 틀이다. 몽구스로 어떤 데이터를 다룰려면 항상 스키마와 모델을 가장 먼저 정의해야한다.
`String,Number,Boolean,Date, default 프로퍼로 기본값을 설정할수있다.`
`timestamps: true`를 사용하면 `createdAt,updatedAt` 필드를 몽구스가 알아서 생성하고 관리할수있다.
- required: 데이터를 생성할 때 꼭 있어야 하는 필드이다.
- maxLength,minLength, enum(특정값중 하나여야 할때)),match(특정 패턴이어야 할때)
- validator: 커스텀 유효성검사필드
```json
validate: {
	validator: function(title ){
		return title.split(' ').length > 1;	
	},
	message: 'Must contain at least 2 words.',
},
```

**CRUD**
.create
```js
app.post('/tasks', async(req,res) => {
	const newTask = await Task.create(req.body);
	res.status(201).send(newTask);
})
```
.find() - 조회
```js
app.get('/tasks', async(req,res) => {
	const tasks = await Task.find();
	res.send(tasks);
})
```
.findById() - id로 조회할때
```js
app.get('/tasks', async(req,res) => {
	const tasks = await Task.findById(req.params.id);
	res.send(tasks);
	} else {
		res.status(404).send({ message: 'Cannot find given id.'});	
	}
});
```
정렬과 개수 재한
.sort() .limit()
```js
app.get('/tasks', async(req,res) => {
	const sort = req.query.sort;
	const count = Number(req.query.count) || 0 ;
	
	const sortOption = {createAt: sort === 'oldest' ? 'asc' : 'desc'};
	const tasks = await Task.find().sort(sortOption).limit(count)
	
	res.send(tasks);
})
```
Update
.save()
```js
app.patch('/tasks/:id', async(req,res) => {
	const id = Number(req.params.id);
	const task = await Task.findById(id)

	if(task) {
		Object.keys(req.body).forEach((key) => {
			task[key] = req.body[key]
		});
		await task.save();	
		res.send(task);
	} else {
		res.status(404).send({ message: 'Cannot find given id'});
	}
});
```
Delete
.findByIdAndDelete - 객체를 가져오는 것과 동시에 삭제한다.
```js
app.delete('/tasks/:id', async(req,res) => {
	const task = await Task.findByIdAndDelete(Number(req.params.id));
	if(task) {
		res.sendStatus(204);	
	} else {
		res.status(404).send({ message: 'Cannot find given id.'});
	}
})
```
비동기 코드
비동기 코드에서 오류가 나면 서버가 죽기때문에, 따로 처리해줘야한다.
모든 핸들러를 감싸는 `asyncHandler()`정의하고 안에 try,catch
```js
function asyncHandler(handler) {
	return async function(req,res) {
		try {
			await handler(req,res);	
		} catch(e) {
			//e.name, e.message;	
		}
	}
}

// ...

app.get('/tasks', asyncHandler(async(req,res) => { ... }));
```
