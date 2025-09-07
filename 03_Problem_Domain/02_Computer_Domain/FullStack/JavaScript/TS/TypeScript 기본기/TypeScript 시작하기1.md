## typescript 기본기
자바스크립트에서는 오타로 문제가 발생하는경우가 적지않다. 그러나 이런오류는  실행도중에 잡아야되는데 이러한 오류는 런타임 오류라고 한다. 프로그램 실행 도중에 발생하는 오류이다.
자바스크립트 언어특성상 코드가 실행되기전 올바른지  검사하지않기 때문에 그렇다.

컴파일언어가 아니라 인터프리터 언어이기때문이다.
```js
let numx = [1,2,3,4];
// 한참 지난 후...
nums = 5;
// 한참 지난 후....
nums.length // 오류 발생!
```
타입스크립트는 이러한 동적 타이핑 언어인 자바스크립트에 정적 타이핑을 지원했다. 코드를 실제로 배포하기 전에 타입 체크 VS Code같은 에디터를 활용하기 좋다.
자바스크립트의 기존 문법을 포함하는것을 슈퍼셋이라고 한다.
- TypeScript 프로젝트 만들기
- 기본적인 타입들
- Enum,  InterFace, 타입 별칭
- Generic
- tsconfig.json
## ts 프로젝트 만들기
```bash
# typescript는 dev옵션으로 만든다.
npm install --save-dev typescript
```
```bash
# 초기 설정파일 만들기
# npm exeute typescript javascript --init
npx tsc --init
```
```json
// 이것을 실행하면 ts문법을 자바스크립트 문법으로 바꿔준다.
"scripts" : {
	"build" : "tsc"
}
```

## TS가 실행되는 과정
타입스크립트 컴파일러(TSC), 트랜스파일(Transpile)
타입스크립트 코드를 자바스크립트 코드로 트랜스파일  해 주는 프로그램

1. 타입검사 (Type Check)
	1. 오타, 타입이 잘못되면 -> 에러메시지를 보여줌
2. 트랜스파일(Transpile)
	1. tsconfig.json에서 맞는  es버전으로  맞춰준다.
3. 맞춰졌다면 node나 웹브라우저에서 이 코드를 실행
	1. 자바스크립트 엔진을 사용해서 실행

## 타입을 정하는 법
```ts
/** 추론을 통해 타입을 정하는 법 */
let size = 100; // number로 타입이 정해집
size = 'L' // 당연히 타입을 변경시킬라카면 오류가 튀어나온다.
//vscode에서 미리미리 타입오류를 잡을수있다.

/** 명시적으로 하는법 */
//let size: number = 100; 
// 곧바로 타입을 정해주지않을때
let size: number;
size = 100;
// 이제 컴파일해보면 number는 타입스크립트 고유문법이기에 사라진다.
// 타입은 컴파일할때만 쓰고 실제 코드를 싦행할때 쓰이지않습니다!
```

## 타입 오류 이해하기
```ts
/*
	오류 코드가 길어도 겁먹지않아도되는게 맨위에는 전체 아래로 갈수록 오류메시지를 좁힌다.
	// 1줄은 들어오는 코드가 안맞다는 것
	Type '{ id: string; name: string; price: number; sizes: number[];}',
	// 2줄은 객체 안에서도 sizes라는 프로퍼티가 안맞다는 것
	Types of property 'sizes' are incompatible.
	// 3줄은 숫자배열을 문자배열에 할당할수없다는것
	Type 'number[]' is not assignable to type 'string[]'.
	// 4마지막줄은 더 좁게 들어간것이다. 숫자열을 문자열에 할당할수없다는 의미이다.
	Type 'number' is not assignable to type 'string'. ts(2322)
*/
```