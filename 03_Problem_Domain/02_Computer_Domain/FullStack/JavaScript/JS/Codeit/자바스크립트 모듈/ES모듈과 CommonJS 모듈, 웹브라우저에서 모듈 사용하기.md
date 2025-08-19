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