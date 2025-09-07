## 기본형
```ts
let itemName: string = '코드잇 블랙 후드';
let itemPrice: number = 129000;
let membersOnly: boolean = true;
let owner: undefined = undefined;
let seller: null = null;

// 아래 두값은 숫자형이다. 
let num = 2/0; // Infinity
let num = 0/0;  // NaN
// 더 깊이 검사할려면 타입메서드에 is 메서드를 활용해야한다.

// seller = undefined    null과는 다른타입이라는것 

```

## 배열과 튜플
```ts
const cart: string[] = [];
cart.push('c001');
cart.push('c002');
//  cart.push(3); 이런식으로 갑자기 문자열을 할당할려고하면 오류가날것이다.

// 배열 타입에는 배열의 크기가 정해지지않습니다.
const carts: string[][] = [
	['coo1','coo2'],
	['coo3'],
];

// 밑에처럼 여러개를 넣어도, 한개를 넣어도, 아무것도 안넣어도 타입오류가 안나온다.
let mySizes: number[] = [162,28];
mySize = [162,27,265];
mySize = [255];
mySize = [];

// 배열이지만 값을 정해줄때 튜플로  정해주면된다.
// 튜플안에 개수와 타입이 맞지않으면 타입오류가 나옵니다
let mySizes: [number, number] = [162,28];
//mySize = [162,27,'asd'];
//mySize = [255];
//mySize = [];

// 이런식으로도 가능합니다.
// let mySizes: [number, number, string] = [162,28,'M'];

```
## 객체 타입
```ts
// 프로퍼티를 만들때  타입을 지정한다는점이 차이점이다.
// vscode에서 템플릿을 띄워주니 훨씬 코딩하기 편해진다.
let product: {
	id: string;
	name: string;
	price: number;
	membersOnly?: boolean;
	sizes: string[];
} = {
	id: 'c001',
	name: '코드잇 블랙 후디',
	price: 129000,
	membersOnly: true,
	sizes: ['M', 'L', 'XL'],
};

// 이렇게 필수가 아닐때 ? 를써주면 그값은 옵셔널한 값이된다.
if (product.membersOnly) {
	console.log('회원 전용 상품');
} else {
	console.log('일반 상품');
}

// 프로퍼티 이름에 변수를 쓰고싶으면 대괄호를 써서 값을 넣습니다
let field = "field name";
let obj = {
	[field]: "field value",
};

// 프로퍼티 이름으로 아무 문자열을 쓸수있게 정해주었고 프로퍼티의 값이 숫자형이다. (참고로 id말고 다른 이름을 아무거나 넣어줘도된다.)
let stock: {
	[id: string]: number
} = {
// 이런식으로 숫자형인 프로퍼티를 추가할수있습니다.
	c001: 1,
	c002: 3,
	c003: 1
}
```
## any
타입스크립트를 사용하는이유는 오류를 미리발견하는것
```ts
// 이런식으로 js 똑같이 할수있지만 의미가없다. 그래서 되도록 사용하지않는것 
const product: any {
.../// 
}

// 물론 파싱할때 any가 들어가는 경우가 있지만 이마저도 타입을 정해주는것이 좋다.
// 어쩔수 없이 몰라서 any타입이 적히는 경우도 많고
const paresedProduct: {
	name: string;
	price: number;
} = JSON.parse(
	"{ "name": "코드잇 토트백", "price": 12000 }"
);
// 아니면 이런식으로 추론시킬수있다.
const paresedProduct = JSON.parse(
	"{ "name": "코드잇 토트백", "price": 12000 }"
) as {
	name: string;
	price: number;
}
// 꺽쇠도 사용가능한데 프론트엔드에서 꺽쇠를 많이쓰는 추세로 이제는 문법때문에 사용하지는않음
const paresedProduct = <{
	name: string;
	price: number;
}>JSON.parse(
	"{ "name": "코드잇 토트백", "price": 12000 }"
);
```

## 함수에 타입 정의하기
```tsconfig.json
"strict": true, // 이 옵션이 켜져있으면
"noImplicitAny": ture // 이 옵션이 켜진다. 암묵적으로 any사용을 금지시킴
```
```ts
// 함수 파라미터에 타입을 명시하고 기본값으로 1을 넣어줌
function addToCard(id: string, quantity: number = 1) {
	if (stock[id] < quantity ) {
		return false	
	}
}
```

 프로퍼티안에 함수를  넣을때 이렇게 하면된다.
 ```ts
 const codeitmall: {
	 stock: {[id:string]: number };
	 cart: string[]; 
	 addToCart: (id: string, quantity?: number) => boolean;
	 addManyToCard: (...ids: string[]) => void;
 } = {
	stock: {
		c001: 3,
		c002: 1,	
	},
	cart: [],
	addToCard,
	addManyToCard,
 };
 
// 아무것도 리턴하지 않는 함수를 void라고 한다. 
 function addManyToCart(...ids: string[]) {
	for (const id of ids) {
		addToCard(id);	
	} 
 }
 ```

## 정리
```ts
//  각 프로퍼티는 세미콜론으로 구분한다. 필수가 아닌 프로퍼티는 프로퍼티 이름 뒤에 물음표를 붙인다.
let stock: {  [id:string]: number} = {
	c001: 3,
	c002: 2,
	c003: 2,
};
```

**any타입**
```ts
const parsedProduct = JSON.parse('{ "name": "코드잇 토트백", "price": 12000 }') as { name: string; price: number };

```
```ts
const parsedProduct: { name: string; price: number } = JSON.parse('{ "name": "코드잇 토트백", "price": 12000 }');

```

**function type**
리턴 타임을 지정하는 경우에는 다음 코드처럼
```ts
function addToCard(id: string, quanity: number): boolean {
	if (...) {
		return false;	
	}
	
	return true;
}
```
리턴 타입을 미리 주지 않고 리턴 값으로부터 추론하게 할 수 있다.
```ts
function addToCart(id: string, quanity: number) {
	if (...) {
		return false;	
	}
	
	return true
}
```
함수를 값으로 사용하는 경우 화살표 함수처럼 작성
```ts
(id: string, quanity: number) => boolean
```
Rest파라미터는 배열 타입으로 쓴다. 값을 리턴하지 않는 경우 리턴 타입을 Void 로 할수있다.
```ts
(...ids: string[]) => void;
```