```js
/* CommonJS */
const calculator = require('./calculator.js');

function circle(x) {
	return calculator.PI * x * x;
}
function square(x) {
	return x * x;
}

module.export = {
	circle,
	square,
};
// Node.js에서만 사용 가능( 웹 브라우저에서 사용 불가능)
// CommonJS모듈이 디폴트이기때문에 .mjs확장자 또는 다른 설정 필요
// 모듈 = 불러올 수 있는 파일 또는 디렉토리
```
```js
/* ECMAScript (ES 모듈) */ //에크마스크립트
import { PI } from './calculator.mjs';

function circle(x) {
	return PI * x * x;
}
function square(x) {
	return x * x;
}

export default {
	circle,
	square,
};
// 2015년에 소개된 문법
// 브라우저와 Node.js에서 모두 사용
// 모듈 = ES 모듈 = 모듈 파일 하나
```
