## interface
똑같은 타입을 여러번 지정하면 유지보수측면에서 썩좋은 코드가아니다.
```ts
// 보통 대문자로 시작하는게 보통이다.
// 상품의 특징이 추가되도 오류가 바로 떠버리니 유지보수하기 좋다.
interface Product  {
	...
}

// 또한 상속이 가능
interface ClothingProduct extends Product {
	sizes: Size[];
}

// 기본적으로 Product의 부모의 타입을 물려받았기에 그대로 나머지는 Product로  지정해줘도 된다.
const product1: ClothingProduct {
	...
}
const product1:  Product {
	...
}

// 함수의  타입도 명시해줄수있다..
interface PrintProduct {
	(product: Product): void
}

/*
function printProduct (product: Product) {
	console.log(`.....`)
}
*/

// 변수로 바꾸면 이런식으로 사용할수있다
const printProduct: PrintProduct = (product) => {
	console.log('...')
}
```