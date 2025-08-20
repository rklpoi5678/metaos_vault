## Promise.all()
여러 Promise를 동시에 기다릴때 사용한다.(promise들을 병렬적으로 처리하고싶을때)
```js
const promises = [];

for (let i = 1; i < 11; i++) {
	promises.push(getEmployee(i));
}

Promise.all(promises)

const employees = await Promise.all(promises);
console.log(employees);

/** 이렇게 try,catch문 사용가능
	let employees;
	
	try {
		employees = await Promise.All(promises);
	} catch (error) {
		console.log('Error')
	}

	console.log(empolyees)
 */

```
![[Pasted image 20250820151952.png]]
![[Pasted image 20250820152032.png]]

## 추가로 성공 여부를 각각 배열로 받고 싶다면
Promise.all() 아닌 Promise.allSettled()를 사용하면 각 promise의 결과를 배열로 반환시킨다.
