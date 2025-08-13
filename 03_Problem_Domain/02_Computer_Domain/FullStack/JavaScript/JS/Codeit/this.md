## 핵심
this는 window객체이다. 객체의 메소드를 만들때 중요한 역할을한다.
아래 코드를 보자
```js
function getFullName() {
	return `${this.firstName} ${this.lastName}`
}

const user = {
	firstName: 'Tess',
	lastName:'Jang',
	getFulName: getFullName,
};

const user = {
	firstName: 'Tess',
	lastName:'Jang',
	getFulName: getFullName,
};


```