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
	response.send(req.query)
	// id값으로 123이 들어올것이다. 파람스로 사용가능해집니다.
	// 쿼리스트링이 있다면 해당 쿼리도 같은 객체에 담기게된다.
}

export default function handler(request, response) {
	response.send(req.body)
	// request로 오는 바디값을 알수있다.	
	// POST ....
}

export default function handler(request, response) {
	response.send(req.cookies)
	// request로 오는 쿠키값을 알수있다.	
}

export default function handler(request, response) {
	response.send(req.method)
	// request로 오는 메서드(GET..POST...)을 알수있다.	
}

// switch문으로 메서드별로 설정해줄수도있다.
export default function handler(request, response) {
	switch(req.method) {
		CASE 'PATCH':
			res.send('short Link 수정);	
			break;
	}
}
```

## 리스폰스 다루기
```js
export default function handler(req, res) {
	switch(req.method) {
		CASE 'POST':
			res.status(201).send({
				title: 'wike Next.js',
				url: 'https://....',	
			});
			break;
			
		CASE 'GET':
			res.send([
				{
					id: 'abc',
					title: 'wike Next.js',		
					url: 'https:....'	
				},
				{
					id: 'abc',
					title: 'wike Next.js',		
					url: 'https:....'	
				}
			]);
			break;
			
		default: 
		// 메소드에 메소드를  메소드체이닝이라고한다.
		// 메소드의 객체값이 메소드그 자체라서 체이닝을할수있다.
			res.status(404).send();
	}
}
```

## 리퀘스트 핸들러 함수
`/api/short-links`로 들어오는 리케수트르르 처리하려면  
`/pages/api/short-links.js`
`/pages/apu/short-links/indes.js`  경로로 파일을 만들고 아래처럼 함수를 default export하면 된다.
```js
export default async function  handler(req,res) {
	...
}
```
- method: 문자열, 리퀘스르로 들어온 메소드값
- query: 객체, 쿼리 스트링이나 Next.js에서 사용하는  Params값이  들어있는 객체
- body: 자유로움, 리퀘스트의 바디 값
- cookies: 객체, 리퀘스트의 쿠키가 키/밸류로 들어있는 객체

## 리스폰스 객체
함수 체이닝 방식으로 사용하기 떄문에 `res.status(201).send()` 처럼 함수를 이어서 사용할수있다.
- status(): 함수, 리스폰스로 보낼  HTTP상태 코드를 지정
- send(): 함수, 리스폰스로 보낼 바디를 전달
