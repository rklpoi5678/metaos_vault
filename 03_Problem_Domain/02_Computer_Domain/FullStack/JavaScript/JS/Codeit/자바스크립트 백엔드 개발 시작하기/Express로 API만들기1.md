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
/** rend메소드가 tasks를 파싱해준다. */
app.get('/hello', (req,res) => {
	res.rend(tasks);
})
```