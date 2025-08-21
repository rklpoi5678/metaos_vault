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
	const id = tasks.map((task) => task.id);
	newTask.id = Math.max(...ids) + 1;
	newTask.isComplete = false;
	newTask.createdAt = new Date();
	newTask.updatedAt = new Date();
	tasks.push(newTask);
	res.status(201).send(newTask);
	
});
```

