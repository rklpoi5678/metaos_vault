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
const data = 'await' response.json() 

// console.log(await.json(response))
```
Promise는 3가지중하나의 상태를 가진다.
pending: 비동기 작업의 결과를 기다리고있을때
fulfiled: 비동기 작업이 성공적일때 (결과값을 리턴해준다.(값을 받아올수있다.))
// awiat는 pending이 fullfiled될때까지 기다린다. 
rejected: 비동기 작업이 중간에 실패했을때

## async
```js
// async함수를 넣어줘야 await에 빨간줄이 안보인다.
export 'async' function printEmployee(){
	const response = await fetch...
	const data = await resposen.json()
}
// async함수는 await의 Promise결과가 fullfild가 될때까지 기다리면서 나머지것을 실행하여
// 아래main.js console이 먼저찍히게된다.

//main.js
import {printEmployees} from './asyncFunctions.js';

printEmployees();

console.log('2');
console.log('3');

```
> await에서 리스폰스를 받을동안 함수밖으로나가서 다른코드를 실행하며
> await을 만날때마다 이 행동을 반복한다.

ArrowFunction을 사용한다면?
```js

export const printEmployeer = async () => {
	....
} 
```

## 효율적인 비동기 코드
비효율적인 코드
```js
export function printEmployees() {
	for(let i=1; i< 11; i++) {
		const response = await fetch('https://learn.codeit.kr/api/employ')
	}
}
```