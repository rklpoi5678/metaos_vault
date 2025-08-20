## Promise란
```js
const response = fetch('...');
console.log(response);
```
- 비동기 작업이 완료되면 값을 알려주는 객체
- 작업이 완료되면 값을 알려줄 것을 '약속' 함
- 일단 Promise를 돌려주고 나중에 작업이 완료되면 결과값을 Promise에 채워 넣어줌
```js
 // 직업 데이터를 가져온 후 리스폰스를 파싱하고 데이터를 프로세싱 하는 예시
 getEmployee((response) => {
	 json(response, (data) => {
		 groupEmployees(data, (result) => {
			 console.log(result)
		 });
	 });
 });
```
Promise사용시
우리가 사용하면 방식으로 코드를 작성할수있는것ㅇ
```js
const response = await fetch('...');
const data = await response.json()
console.log(data);
```