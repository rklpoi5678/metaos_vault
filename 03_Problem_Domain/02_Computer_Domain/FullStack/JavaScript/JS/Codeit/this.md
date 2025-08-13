## 핵심
this는 window(전역객체)객체이다. 객체의 메소드를 만들때 중요한 역할을한다. (메소드,프로퍼티에 자주사용)
아래 코드를 보자
```js
function getFullName() {
	return `${user.firstName} ${user.lastName}`
}

const user = {
	firstName: 'Tess',
	lastName:'Jang',
	getFulName: getFullName,
};

const admin = {
	firstName: 'Alex',
	lastName:'Kim',
	getFulName: getFullName,
};

console.log(user.getFullName());
console.log(admin.getFullName())
// 이럴때 문제가 생기는데 user을 가리키고 있어 둘다 콘솔에는 Tess Jang이 찍힌다.
// 그러므로 이럴때 this 문법이 유용하다. this는 함수를 호출한 객체를 가리키는 키워드이다.

function getFullName() {
	return `${this.firstName} ${this.lastName}`
}
```
> 상대적으로 값이 변하게 된다는 것이 특징이다.
> 기본적으로 this는 객체를 가리키게 되고 메서드를 호출하면 함수를 호출하면 객체가 this에 담기기 때문에 똑같은 함수를 호출했지만 콘솔에는 각각 다른 객체가 출력된다.

## 일반 함수선언 과 arrowfunction으로 사용했을때차이
화살표함수로 선언하면 화살표함수선언과 동시에 this에 똑같은 값을 가지고 동작하게된다.
화살표함수가 선언되기 이전에 this는 window객체 그래서
이런 특징 때문에 특별히 객체에 메소드를 만들때는 일반함수가 좀 더 권장된다.
