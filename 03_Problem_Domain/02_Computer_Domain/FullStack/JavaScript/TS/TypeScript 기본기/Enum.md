## Enum(열거형)
상품 사이즈처럼 값을 나열할수있는경우 이넘을 사용한다.
```ts
enum Size {
	S,
	M,
	L,
	XL
}

let product: {
	id: string;
	name: string;
	price: number;
	membersOnly?: boolean;
	// type으로 쓸때는 이넘이름만
	sizes: Size[];	
} = {
	id: 'c001',
	name: '코드잇 블랙 후디',
	price: 129000,
	// 값으로 쓸때는 객체처럼 점표기법으로 쓰면된다.
	sizes: [Size.M, Size.L],
};

// 이넘의 기본값은 0부터 시작하게 되니 주의해야한다.
if (!size) {
	// 즉 0 부터 시작하니 0은 예상치도 못하게 이 구문으로 들어오지못할수있다. 
}

/* 그래서 되도록 enum을 쓸때는 값을 정해놓고 사용한다.*/
enum Size {
	S = 'S',
	M = 'M',
	L = 'L',
	XL = 'XL;,
}
// 이제 다시 콘솔로 찍어보면 값이 있는 경우랑 없는경우랑 구분이 잘되게 된다.
```
> 숫자 0은 실수하기 쉽기 떄문에 Enum을 사용할 땐 되도록이면 값을 정해놓고 사용하는게 좋다. 이퀄이랑 쉼표를  쓰면 값을 정할 수 있다.