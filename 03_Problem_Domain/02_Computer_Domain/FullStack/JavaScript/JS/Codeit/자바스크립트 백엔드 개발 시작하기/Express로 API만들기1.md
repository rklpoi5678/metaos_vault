## Subscription API
예시
```json
{
  "_id": "641bf3c9c0a964b65289902a",
  "name": "넷플릭스 프리미엄",
  "price": 17000,
  "cycle": "m",
  "firstPaymentDate": "2021-07-01T00:00:00.000Z",
  "memo": "10일날 취소하기",
  "createdAt": "2023-03-23T06:34:11.617Z",
  "updatedAt": "2023-03-23T06:34:11.617Z"
}
```

## express.js
```js
import express from "express";

const app = express();

// 들어오는 객체 나가는 객체
app.get('/hello', (req,res) => {
	res.send('Hello Express');
}); 

// 포트 3000번을 듣고 3000번이면 콘솔을 출력해라
app.listen(3000, () => console.log('Server Started'));
```

### **requests.http**
restClient에서는 http확장자를 사용합니다.
```http
GET http://localhost:3000/hello
```
> vscode플러그인을 사용해서 Send Request버튼을 클릭하면 리스폰스를 알려준다.

### **nodemon**
서버를 새로고쳐야지 변화가 생기는데 노드몬은 바로 응답이 가능하게 만들어주는 라이브러리이다.
```json
...
// 개발환경에서는 노드몬으로. 프로덕션 환경에서는 노드로 실행할것이다.
"scripts" : {
	"dev": "nodemon app.js",
	"start": "node app.js"
}
// npm run dev
```

## GET 리퀘스트 처리하기
\+ 테스트 데이터를 mock데이터라고도 많이부른다.
```js
/** 
rend메소드가 tasks를 파싱해준다.
또한 send메소드가 자동으로 header도 잡아주기에
웹 API를 만들때 많이사용한다.
 */
app.get('/hello', (req,res) => {
	res.send(tasks);
})
```

## 쿼리스트링 처리하기
```http
GET http...

requests.http에서는 리퀘스트를 구분할려면 ###를 써줘야한다.
###

쿼리스트링을 쓰는방법이다.
GET http.../tasks?sort=oldest&count=5
```
```js
/*
	쿼리 파라미터
	- sort: 'oldest'인 경우 오래된 태스크 기준, 나머지 경우 새로운 태스크 기준
	- count: 태스크 개수
*/

app.get('/tasks', (req,res) => {

  const sort = req.query.sort;
  const count = Number(req.query.count);

// sort가 oldest면 a기준으로 양수이면 오름차순 음수이면 내림차순 
  const compareFn =
    sort === 'oldest'
      ? (a,b) => a.createdAt - b.createdAt
      : (a,b) => b.createdAt - a.createdAt;
  
  let newTasks = tasks.sort(compareFn);
	
	if(count) {
		newTasks = newTasks.slice(0, count);
	}
      
  res.send(tasks);
});
```

## 다이나믹 URL 처리하기
URL이 항상일정하기 않고 일부가 바뀌는것을 의미한다.
```js
// :id이 동적 파라미터라고 한다. 이 부분은 params로 전달된다.
// params 프로퍼티로 url객체들이 전달되는것이다.
// 기본적으로 문자열이다.(그래서 Nubmer로 행변환을 해야될경우도 있다)
app.get('/tasks/:id', (req,res) => {
	const id = Number(req.params.id);
	// 항당 아이디를 이용해서 tasks의 아이디를 찾는다.
	const task = tasks.find((task) => task.id === id);
	
	//id가 없을수도 있으니
	if(task) {
		res.send(task);
	} else {
	// status를 이용해서 404일시 해당 오류메시지를 출력하도록 할수있다.
		res.status(404).send({ message: 'Cannot find given id'})	
	}
	
});

app.listen(3000, () => console.log('Server Started'));
```