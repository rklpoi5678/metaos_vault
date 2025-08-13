## 핵심
기본은 이름이없는 익명함수이다(그러므로 변수에 할당하거나 다른 함수를 호출할 때 아규먼트로 사용된다는 점을 잘 기억해야된다.). ES6부터 지원하는 문법이다.
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

const getCodeit = () => {
	return { name: 'Codeit', }
}

/** 위에서 리턴문이 하나이고 리턴내용이 객체일때는 소괄호로 한번더 감싸주면된다.*/
const getCodeit = () => ({ name: 'Codeit', })


/** 파라미터가 두 개 이상이거나 없을땐 소괄호를 무조건 넣어야한다. */
myBtn.addEventListener('click', () =>{
	console.log('button is clicked!')
})
```
> 추가로 arrowfunction에는 arguments가 없다 그러므로 arguments를 arrowfunction으로 대체하기는 어렵다는 점 참고