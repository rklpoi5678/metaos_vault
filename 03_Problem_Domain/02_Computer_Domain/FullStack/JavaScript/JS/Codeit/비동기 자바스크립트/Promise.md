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
우리가 사용하면 방식으로 코드를 작성할수있는것이 큰장점
많은 자바스크립트에서 비동기 코드로 Promise를 활용하는 이유이다.
```js
const response = await fetch('...');
const data = await response.json()
console.log(data);
```

## await 문법
```js
// fetch가 완료될때 response에 할당해준것
const response = await fetch('..')
// json으로 파싱할때도 오래걸릴수있기에 await을 안넣으면 Promise를 리턴
const data = 'await' json(response)

// console.log(await.json(response))
```
Promise는 3가지중하나의 상태를 가진다.
pending: 비동기 작업의 결과를 기다리고있을때
fulfiled: 비동기 작업이 성공적일때 (결과값을 리턴해준다.(값을 받아올수있다.))
// awiat는 pending이 fullfiled될때까지 기다린다. 
rejected: 비동기 작업이 중간에 실패했을때

