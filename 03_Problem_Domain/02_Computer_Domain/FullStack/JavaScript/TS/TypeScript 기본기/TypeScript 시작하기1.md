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