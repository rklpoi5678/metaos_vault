## Mongoose란?
쉽고 편리하기 떄문에 MongoDB를 사용하는 자바스크립트 개발자들이 가장 많이 사용하는 라이브러이다.

## 환경 변수사용
Next.js에서는 기본적으로 dotenv라는 라이브러리를 지원한다. 이 라이브러리는 .env같은 이름의 파일에서 환경 변수들을 저장해 두면, Node.js프로젝트를 실행할때 환경 변수로 지정해 주는 라이브러리이다.
```js
MONGODB_URI=mongodb+srv://admin:blahblah@.clusterName.blahblah.mongodb.net/databaseName?retryWrites=true&w=majority
```
```js
export default function handler(req,res) {
	const DB_URI = process.env.MONGODB_URI;
	// 데이터베이스 접속
}
```
next.js 에서는 웹 사이트로 환경변수가 노출되는것을 막기위해 클라이언트 사이드에서 사용하는 환경 변수에 특별한 접두사(prefix)를 사용한다. `NEXT_PUBLIC_`이라고 이름을 붙이면 이 환경 변수는 클라이언트 사이드에서도 사용할 수 있다.
```js
MONGODB_URI=mongodb+srv://admin:blahblah@cluster0.blahblah.mongodb.net/databaseName?retryWrites=true&w=majority
NEXT_PUBLIC_HOST=http://localhost:3000
```
```js
export default Home() {
	// 페이지 컴포넌트에서는 아래와 같이 사용
	return (
		<>호스트 주소: {process.env.NEXT_PUBLIC_HOST}</>	
	)
}
```