## try catch로 오류 처리하기
```js
export async function printEmployees(){
	try {
		const response = await fetch('//');
		const data = await response.json();
		console.log(data);
	} catch (error) {
		console.log('Error!');
		//return;
	} //finally { 만약 에러시 리넡이된다면 finally는 그것을 무조건실행한다.
		//console.log('Finished')  정상적이여도 finally는 무조건실행
	}
	console.log('Finished');
	// 주소값이 이상할경우 catch문이 잡고 code-0으로 종료된다. 
}
```
> Promise가 rejected상태일때는 오류를 throw한다.
> 프로그램의 필요에 따라 더 적절한 방식으로 오류를 처리하면 된다.

## Promise와 오류 제대로 이해하기
Rejected 
![[Pasted image 20250820142848.png]]
먼저 기다리고 있는동안 함수밖코드를 실행하는데 Promise는 2가지중하나를 반환할것이다.
풀필드상태일때는 리스폰스를 반환하지만, 리젝트상태는 코드를 트로우한다. 이제 try-catch문이 있기에 catch가 던지는것을 잡아주는것
> 이러한 방식덕분에 비동기 형식을 동기형식으로 만들수있던것

```js
async function printEmployees() {
	const response = await fetch('```');
	const data = await response.json();
	console.log(data);
}

// 위 코드를 then으로 표현하면
const d
```