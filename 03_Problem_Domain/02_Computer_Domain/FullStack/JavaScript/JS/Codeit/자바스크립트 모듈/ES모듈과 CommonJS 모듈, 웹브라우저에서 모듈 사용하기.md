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
```