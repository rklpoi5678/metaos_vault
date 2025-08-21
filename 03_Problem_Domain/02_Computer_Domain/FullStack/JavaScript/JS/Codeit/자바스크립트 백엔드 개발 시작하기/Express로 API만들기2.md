## POST 리퀘스트 처리하기
```http
// 리퀘스트는 POST바로 아래 내용을 쓰면된다. body는 한줄띄우고 써야한다.
POST http://localhost:3000/tasks
Content-Type: applicaiton/json

{
	"title": "강아지 산책",
	"description": "강아지랑 30분 산책하기"
}
```
express는 바디로 전달된 json을 자동으로 자바스크립트 객체로 변환해주지않습니다.
json -> JS Obj로 변환하는 과정을 parsing이라고 한다.
express.json이라는 함수를 사용해야합니다.
```js
// express전체에서 express.json()을 사용하겠다는 선언
app.use(express.json());

app.post('/tasks', (req,res) => {
	const newTask = req.body;
	// 이부분은 DB가 있다면 더 쉬워진다.
	// task아이디 모든값을 찾아서 1을더해줌
	// 새로생성된것이니 완료는 폴스
	// 현재시간으로 설정
	// post하면 생성된 바디와 리스폰스를 돌려준다.
	const ids = tasks.map((task) => task.id);
	// task에 있는 아이디의 값을 찾아 1을 더합니다.
	newTask.id = Math.max(...ids) + 1;
	newTask.isComplete = false;
	newTask.createdAt = new Date();
	newTask.updatedAt = new Date();
	tasks.push(newTask);
	res.status(201).send(newTask);
});
```

## PATCH 리퀘스트 처리하기
```http
...
// 일부 수정할 프로퍼티부분을 적어주면된다.
###

PATCH http:localhost:3000/tasks/1
Content-Type: application/json

// request.body부분에 들어갈 내용
{
	"isComplete": true
	/* 
		// 이런식으로 여러 필드를 넣어줄수도 있다.
		"title" : "1시간 운동",
		"description": "열심히 운동하기"
	 */
}
```
```js
app.patch('/tasks/:id',(req,res) => {
	const id = Number(req.params.id);
	const task = tasks.find((task) => task.id === id);
	// task와 req.body에있는 task key가 같을때 
	// 리스폰스를 돌려줌
	if(task){
		Object.keys(req.body).forEach((key) => {
			task[key] = req.body[key]
		});
		task.updatedAt = new Date(); //수정된 날짜를 업데이트해줘야한다.
		res.send(task);
	} else {
		res.status(401).send({ message: "Cannot find given id"});
	}
});
```

## Delete리퀘스트 처리하기
```http
딜리트는 특정 테스크를 없애는거기에 바디가 필요없겠다.

DELETE http://localhost:3000/tasks/1
```
```js
app.delete('/tasks/:id', (req,res) => {
	const id = Number(req,params,id);
	const idx = tasks.findIndex((task) => task.id === id);
	// index idx에서 시작해서 요소 1개를 지워라( 만약 찾지못하면 -1이기에 false)
	// 삭제를 성공시 204상태코드 를 보내고 바디에는 아무것도 담지않는다.
	// 바디에서 어떤 상태코드르 보내고싶을때는 status(204)를 보내면 된다.
	if(idx >= 0) {
		tasks.splice(idx,1);	
		res.sendStatus(204);
	} else {
		res.status(404).send({ message: 'Cannot find given id'})
	}
})
```

## 헤더 살펴보기
```http
POST http://localhost:3000/
Content-Type: aplication/json

...

```
이렇게 리퀘스트에 포함되는 정보가 바로 "헤더" 이다.
여기에는 브라우저의 정보나 리퀘스트 바디의 데이터 형식, 인증 토큰등이 포함될수있다.
> User-Agent나 Content-Type Authorization등이 포함될 수있다.

클라이언트 -> 서버로 함께 전송하는 헤더를 "리퀘스트 헤더"
서바 -> 클라이언트 리스폰스 보낼때 포함하는 헤더를 "리스폰스 헤더"
![[Pasted image 20250821233002.png]]

### **request header**
> req.headers
브라우저에서 보낸 리퀘스트 헤더의 내용을 살펴보면 다양한 헤더가 있는 것을 볼수있다.
```json
{
	host: 'localhost:3000',
	connection: 'keep-alive',
	//...
	'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac Os X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/134.0.0.0 Safari/537.36',
	accept: 'text/html...'
	//...

}
```
> 특정 헤더의 값을 확인하고 싶다면, 아래와 같이 get()메소드에 파라미터로 헤더의 키를 넘겨주면 된다.
```js
req.get('host'); // => localhost:3000
```

### **리스폰스 헤더**
Node.js에서 제공하는 메소드인 res.getHeades()를 사용할수있다.
```js
res.getHeaders();
```
```js
// 개별로 확인 리스폰스 객체의 get() 메소드로 확인 가능
res.get('X-Powered-By') // => Express
```
```js
// 헤더와 다르게 리스폰스는 서버 개발자가 만들어서 클라이언트에 제공해야하는 것이기에 set()메소드로 특정 헤더를 설정할수있다.
res.set('X-Custom-Header','custom-value');
```

### **리스폰스 헤더 주의 사항**
1. res.set()으로 동일한 헤더를 설정하면 마지막 값만 반영
```js
res.setHeader('color','red');
res.get('color'); // red
res.setHeader('color', 'blue');
res.get('color'); // blue
```
2. 헤더는 대소문자를 구분하지 않습니다.
	1. 첫 글자나 하이픈뒤의 첫 알파벳을 대문자로 쓰는 경우가 많지만, HTTP 헤더는 기본적으로 대소문자를 구분하지 않기 때문에 content-type과 Content-Type은 동일한 헤더로 인식


## 정리
```js
// Express 기본 뼈대 
import express import 'express';

const app = express();

app.listen(3000,() => console.log('Server Started')); 
```

### **라우트 정의**
```js
app.method(path, handler);
/*
	method: HTTP 메소드 이름
	path: 엔드포인트 경로
	handler: 핸들러 함수, 첫 번째 파라미터로 리퀘스트 객체, 두번째 파라미터로 리스폰스 객체를 받는다
*/
```

```js
// Arrow Function 핸들러
app.get('/some/path',(req,res) => {
 // 리퀘스트 처리
});
```
```js
// 핸들러 함수 선언
function handler(req,res) {
	// 리퀘스트 처리
}

app.get('/some/path', handler)
```

### **리퀘스트 객체**
`req.query`
쿼리스트링 파라미터를 프로퍼티로 담고 있는 객체이다. 파라미터는 항상 문자열이다.
```js
app.get('/some/path',(req,res) => {
	console.log(req.query); // { foo: '1', bar: '2' };
});
```
`req.params`
URL 파라미터 프로퍼티를 담고 있는 객체. 파라미터는 항상 문자열이다.
```js
app.get('/some/:id/path/:name', (req, res) => {
	console.log(req.params); // { id: '1', name: 'james'}
});
```
`req.body`
리퀘스트 바디내용. 접근시 `express.json()`필요
```json
{
	"field1": "value1",
	"field2": "value2"
}
```
```js
app.use(express.json());

app.post('/some/path',(req,res) => {
	console.log(req.body); // { field: 'value1', field: 'value2' }
});
```
`res.send()`
리스폰스를 보낸다. Content-Type헤더를 설정하고 적절한 바디 내용으로 변환해준다.
API서버를 만들 때는 주로 객체나 배열을 전달
application/json으로 설정하고 객체나 배열을 JSON문자열로 바꿔서 전달해준다. 디폴트 상태코드는 200 OK`
`res.stauts()`
리스폰스의 상태 코드를 설정한다.
`res.sendStatus(`