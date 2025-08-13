## 핵심
기본은 이름이없는 익명함수이다. ES6부터 지원하는 문법이다.
애로우 함수로 더 간결하게 표현할수있다.

```js
/** 기본 사용법이며 function을 arrow로 바꿔주면된다.*/
const getTwice = (number) => {
	return number * 2
};

/** 파라미터가 하나일때 기본적으로 소괄호 부분을 생략할수있다.
* 또한 리턴문이 하나밖에 없을때는 그 return문도 생략이 가능하다.
*/
const getTwice = number => number * 2

/** 파라미터가 두 개 이상이거나 없을땐 소괄호를 무조건 넣어야한다. */
myBtn.addEventListener('click', () =>{
	console.log('button is clicked!')
})
```