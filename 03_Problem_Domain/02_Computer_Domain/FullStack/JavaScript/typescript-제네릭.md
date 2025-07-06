## 핵심
어떤 종류든 다 담을 수 있는 만능 컨테이너와 같다.
함수나 배열같은 자료구조를 만들 때, "나는 여러 종류의 데이터를 다루고 싶은데, 타입 체크는 포기하고 싶지 않아"라고 고민을 할 때가 있다.
- string, number 값도 같이 처리할때가있다
- any타입한계: 타입스크립트의 큰 장점인 타입 체크의 도움을 못받게 되는것
- 중복코드: number을 위한 함수, string을 위한 함수를 각각 만들면 코드가 너무 길어지고 관리가 힘듬

해결책
- "나는 어떤 타입이 들어올지는 모르지만, 일단 그 타입을 기억해뒀다가 나중에 그대로 써먹을 것입니다." 하나의 코드에 여러 타입에 대응하면서도, 타입 체크의 이점을 그대로 유지가능

## 제네릭 사용하기
가장 기본은 `<T>`처럼 꺾쇠 괄호 안에 대문자 알파맷 보통 T 을 넣어서 타입 변수를 선언한다. T가 바로 이 함수가 처리할 미지의 타입으 의미한다.
```ts
function identity<T>(args:T):T {
	return arg;
}
```
T라는 타입의 인자 arg를 받아서, 다시 T타입의 값을 돌려줄 거야, 라는 의미이다.
T가 숫자면 숫자로 문자열이면 문자열을 받아서 문자열로 돌려주는 격이다.
- 함수를 호출할때 `identity<number>(10)`처럼 T가 어떤 타입이 될지 명시적으로 알려줄 수있고, 타입스크립트가 알아서 추론하게 `identity(10)`처럼 사용할수도있다.

## 제네릭 타입 변수 사용하기 (Working with Generic Type Variables)
타입 변수 T는 그냥 '알 수 없는 어떤 타입'이라는 의미이다. 그래서 T 타입의 arg에 arg.length처럼 특정 속성에 바로 접근할 수는 없다.
- 제약조건추가: 만약 T가 특정 속성(에:length)을 가지고 있는 타입이어야 한다면, 제약 조건을 걸어줄 수 있다. T extends Lengthwise처럼 extends키워드를 사용해서 T가 Lengthwise라는 인터페이스를 '확장해야 한다'고 제한하는 것이다.

```ts
interface Lengthwise {
	length: number;
}
function loggingIdentity<T extends Lengthwise>(args: T): T {
	console.log(arg.length); //이제 T는 length 속성을 가짐이 보장되므로 안전하게 접근 가능
	return arg;
}
```
이건 "만능 컨테이너에 물건을 넣을 건데, 무게를 잴 수 있는 물건만 넣어줘!" 라고 제약하는 것과 같아요
```ts
function identity<T>(arg: T[]): T[] {
	console.log(arg.length) // 배열은 .length를 가지고 있습니다 .따라서 오류는 없습니다.
	return arg;
}
```
```ts
function loggingIdentity<T>(arg: Array<T>): Array<T> {
	console.log(arg.length) //배열은 .length를 가진다. 따라서 이것또한 오륜는 없다.
	return arg;
}
```

##  제네릭 타입 (Generic Types)
함수 자체를 제네릭으로 만들 수도 있지만, 함수 타입을 제네릭으로 정의할수있다.
```ts
interface GenericIdentityFn<T> {
	(arg: T): T;
}
//또는 타입 별칭으로
type GenericIdentityFn<T> = (arg: T) => T;

let myIdentity: GenericIdentity<number> = identity;
//myIdentity는 이제 숫자를 받아서 숫자를 반환하는 함수여야만 한다.
```
이건 숫자 전용 물건을 담는 만능 컨테이너 함수라는 타입 자체를 정의하는 것이다.

## 제네릭 클래스(Generic Classese)
클래스안에 있는 프로퍼티나 메서드의 타입을 '미지정 타입'으로 다루고 싶을때 사용한다.
```ts
class GenericNumber<T> {
	zeroValue: T;
	add: (x:T, y:T) => T;
}

let myNumber = new GenericNumber<number>(); //숫자를 다루는 제네릭 클래스
myNumber.zeroValue = 0
myNubmer.add = function(x,y) {retrun x + y; };

let myString = new GenericNumber<string>(); //문자열을 다루는 제네릭 클래스
myString.zeroValue = ""
myString.add = function(x,y) { retrun x + Y; };
```
숫자만 넣을수있는 계산기 틀 또는 문자열만 넣을 수 있는 계산기 틀을 하나의 만능 계산기를 설계도로 만드는것과 같다

## 제네릭 매개변수의 기본 타입( Default Types in Generics )
제네릭 타입 변수에 기본값을 설정할수있다. 만약 사용자가 타입을 지정해주지 않으면 이 기본타입이 사용된다.
```ts
function createArray<T = string>(length:number, value: T): T[]{

}
let numbers = createArray(5, 10); // T는 number로 추론됨
let strings = createArray(3, "hello"); // T는 string으로 추론됨
let defaultStrings = createArray(2, undefined) //T는 string (기본값)
```
만능 컨테이너를 만들건데, 아무 말이 없다면 기본적으로는 문자열을 담는다고 생각할게 라고 미리 정해두는것이다.


---
코드를 재사용 가능하게 만들고, 타입 안정성을 유지하면서, 유연하게 다양한 타입에 대응할 수 있도록 해주는 정말 중요한 개념이다.