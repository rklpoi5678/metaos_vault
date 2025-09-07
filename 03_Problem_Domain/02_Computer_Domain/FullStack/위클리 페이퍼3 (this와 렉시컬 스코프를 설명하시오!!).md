## 핵심
this: (이것) 개발자들은 개으른 성향인 사람과 불편한것을 못참기에 직관적으로  적을려고함
느낌은 알겠으나 헷갈림
```tsx
/** this는 현재 객체나 이것을 가리킨다.*/

console.log(this) //window : 현재 최상위 객체를 가리킨다.

// + 그래서 window.location.href같이 location.href로도 적을수있다.

```

```tsx
const Person = {
	id: Number;
	name: String;
	age: Number;
	hobby: String[];
} = {
	id: 1,
	name: "KimJounUn",
	// ...
}

Person.name // KimJounUn //this  는 점표기법과 같이 접근한다고 보시면됩니다.
```
자바 나 클래스에서는 더 확실
```js
class Persion {
// 여기서 this는 Person을 가리킨다.
// 생성자로 받은 파라미터를 
	constructor(name, age, hobby){
		this.name = name
	}
}
```