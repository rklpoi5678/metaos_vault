## 태그 함수( Tagged Function)
태그 함수를 통해 Styled Components 와 비슷한 함수를 만들고 편리한  문법이 어떻게 만들어진건지 한번 파헤쳐보는시간

태그함수란 템플릿 리터럴 문법을  사용해서 실행할 수 있는 함수이다.(템플릿 리터럴은 내장된 표현식을 허용하는 문자열 리터럴입니다. 이전 버전의 ES2015사양 명세에서는 "template strings" (템플릿 문자열) 라고 불려 왔습니다.)
```js
`string text`

`string text  line 1
 string text  line 2`
 
 `string text ${expression} string text`
 
 tag `string text ${expression} string text`
```


```jsx
function h1(strings, ...values) {
	return [strings, values];
}

const result = h1`color: pink;`;
console.log(result); // [['color: pink;`], []]
```
> h1 에 1파라미터로 스트링, 나머지 파라미터를 밸류 배열로 받는데  템플릿 리터럴로 실행 일반적인 형태로 함수를 선언하고, 템플릿 리터럴로 실행하면 특정한 형태로 파라미터가 전달된다.

```jsx
function h1(strings, ...values) {
	return [strings, values];
}

const backgroundColor = 'black';
const result2 = h1`
	background-color: ${backgroundColor};
	
`
```