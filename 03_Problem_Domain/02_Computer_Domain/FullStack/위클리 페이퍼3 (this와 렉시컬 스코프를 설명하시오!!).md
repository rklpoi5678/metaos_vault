## 핵심
**this: (이것)** 개발자들은 개으른 성향인 사람과 불편한것을 못참기에 직관적으로 적을려고함
지금 **내가 속한 객체를 참조하는 키워드**이다. 
느낌은 알겠으나 헷갈림  왜냐하면  **문맥(Context)에 따라 달라집니다.**
```tsx
/** this는 현재 객체나 이것을 가리킨다.*/

console.log(this) //window : 현재 최상위 객체를 가리킨다.

// + 그래서 window.location.href같이 location.href로도 적을수있다.

```

```tsx
type Person = {
	id: number,
	name: string,
	age: number,
	hobby: string[];
};

const person: Person = {
	id: 1,
	name: "KimJounUn",
	age: 56,
	hobby: ["핵개발","게임"]
}

Person.name // KimJounUn //this  는 점표기법과 같이 접근한다고 보시면됩니다.

// 조금 더 정확하게는  "객체" 안에  자기 자신을 참조할때 주로 사용합니다.
const Person {
	id: 1,
	name: "KimJounUn",
	age: 56,
	hobby: ['핵개발','게임']
	greeting(): {
		console.log(`hello ${this.name}입니다.`)	
	}
}
```
자바 나 클래스에서는 더 확실
```js
class Person {
// 여기서 this는 Person(인스턴스)을 가리킨다.
// const myPerson = new Preson("kim") 즉 여기서 인스턴스 myPerson을 가리킴 
// 생성자로 받은 파라미터를 객체로 지정
	constructor(name, age, hobby){
		this.name = name
	}

	// abstract키워드가 없기에 에러로 강제하는 패턴
	// 추상 메서드 처럼 동작할곳
	speak() {
	// 여기서 쓰지밀고 호출하지말아주세용
		throw new Error ("speak() 메서드는 구현되어야한다.")	
	}
	
	// 일반 메서드는 그대로  요녀석만의 행동	
	move() {
		console.log(`${this.name}이 움직이고있는듯`)	
	}
}

class Baby  extends Person {
...
}
```

**문맥이 변화할때 예시**
```js
function normalFunc() {
	console.log(this); //전역(window)
}

const obj  =  {
	name: "kim",
	arrowFunc: () => {
		console.log(this); // 부모 스코프(window)	
	},
	regularFunc() {
		console.log(this); // 해당 object를 가리킴	
	}
}
```
1. 화살표 함수는 자신만의 this를 가지지않습니다.
2. 선언된 위치에  this를 그대로 가져온다. 즉 실제로는 obj를 생성하는 외부 스코프의 this를 참조(문 안  바깥에서 바깥에서)그 외부 스코프가  전역이기에 window가 됨
3. 일반 함수는 호출될 때 this 가 호출한 주체에 따라 결정이된다.
4. obj.regularFunc()처럼 호출하면 this는 obj를 가리킨다.

---
## 렉시컬 스코프
코드를 적은 위치에 따라 변수의 범위가 결정되는 방식이다.
함수가 어디서 실행(위치) -> 어떤 스코프에 접근할수있을지
어디서 태어났는지 문제이기도 합니다.

결론은 함수스코프, 전역스코프 등등 라고 불리는 그 스코프입니다.
```js
function 밖() {
	const message = '태어났다';
	
	function 안(){
		console.log(message)	
	}
	
	return 안;
}

const 예시 = 밖();
예시(); // 태어났다.
```
 안 함수는 밖 함수 안에서 만들어짐
 그래서 안은 밖안에 있는 메시지변수에 접근가능
 ```js
function 밖 const message; <- function 안() { console.log (messager)}
 ```
 밖에서 안을 실행해도, 자기가 태어난 곳의 변수(message)를 기억하고 있습니다.
```js
const 예시 = 밖()
예시(); // return 을 안으로 했기에 콘솔이 출력됨
```

아래 코드처럼 태어난 위치 기준으로 name=안 에  접근한다.
왜냐하면 태어난 위치 범위기준 밖에 기억하지못한다.
```js
const name = "밖";

function outer() {
  const name = "안";

  function inner() {
    console.log(name); // "안"
  }

  return inner;
}

const fn = outer();
fn(); // "안"

```
자스의 규칙이다.

+ 이것의 적용규칙순서나 스코프들이 연결되어있을때 어떻게 연결되어있는지 보여주는 말을
+ 스코프 체인이라고 한다.