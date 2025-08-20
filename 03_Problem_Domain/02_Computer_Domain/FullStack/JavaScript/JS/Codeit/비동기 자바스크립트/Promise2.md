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
