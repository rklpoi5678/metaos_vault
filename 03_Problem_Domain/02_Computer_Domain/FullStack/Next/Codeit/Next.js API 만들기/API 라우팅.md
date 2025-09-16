##  가이드 
몽고 DB 사용

## API 라우트 만들기
next.js는 폴더처럼 api폴더도 엔드포인트(도착지점)가 된다.
```js
// short-links.js // short-links라는 엔드 포인트
export default function handler(request, response) {
	response.send('안녕 API');
}

// 동적라우팅
// short-links폴더를 만들고 안에 index.js(워코드), [id].js를 만든다.
// [id].js
export default function handler(request, response) {
	response.send('안녕 다이나믹라우팅');
}
```
```http
// 둘다 동작하게된다.
GET https;//.... .com/api

###

GET https;//.... .com/api/123
```

## 리퀘스트 다루기
```js
export default function handler(request, response) {
	response.send(req,query)
	// id값으로 123이 들어올것이다. 파람스로 사용가능해집니다.
	// 쿼리스트링이 있다면 해당 쿼리도 같은 객체에 담기게된다.
}

export default function handler(request, response) {
	response.send(req,body)
	
	// POST ....
}
```