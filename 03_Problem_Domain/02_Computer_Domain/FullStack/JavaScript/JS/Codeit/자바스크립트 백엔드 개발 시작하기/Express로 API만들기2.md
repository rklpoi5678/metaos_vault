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