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
const dataPromise = fetch('```').then((response) => response.json());
dataPromise.then((data) => console.log(data));

// 더간결하게
// then은 프로미스를 리턴하기에 뒤에 then을 또 붙일수있는것 
// 이렇게 연결해서 작성하는것을 **프로미스 체이닝**이라고 한다.
fetch('```')
	.then((response) => response.json());
	.then((data) => console.log(data));
```

![[Pasted image 20250820143629.png]]
pending상태의 리퀘스트를 보낸다.![[Pasted image 20250820143719.png]]
패치에서 가져온 리스폰스값이 전달되면 해당 then은 리스폰스가된다.
![[Pasted image 20250820143822.png]]
파싱된 데이터값이 data파라미터에 들어가면서 콘솔에 출력되고 undefined값이 리턴되어 리스폰스된다. 즉 위에서부터 성공결과값을 전달 전달 값을 가지고 실행이된다는점이다.
