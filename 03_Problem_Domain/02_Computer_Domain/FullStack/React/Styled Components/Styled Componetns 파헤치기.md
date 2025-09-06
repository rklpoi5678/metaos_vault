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
	color: pink;
`;
console.log(result2);
//  [['\n background-color:  ', ';\n color: pink;\n'], ['black']]
```
strings에는 값이 삽입되는 부분 앞뒤로 문자열들이 잘려서 배열로 들어가 있고, values에는 삽입된  값들이 배열로 들어가 있다. 이것이 태그함수의 기본적인 동작이다. CSS스타일이 생성된 리액트 컴포넌트를 만드는 것이 Styled Components의 핵심 아이디어이다.

```jsx
function h1(strings, ...values) {
	// React 컴포넌트를 만든다.
	function  Component({ children }) {
		// 템플릿 리터럴에서 받은 값을 CSS 코드로 만든다.
		 let style = '';
		 for (let i = 0; i < strings.length; ++i) {
			style += strings[i]; 
			if (values[i]) {
				style += values[i];	
			}
		 }	
		 
		 // CSS 코드에 따라 클래스 이름을 만든다.
		 const className = `my-sc-${style.length}`;
		 
		 // `<style>` 태그로 만든 CSS  코드를 렌더링한다.
		 return (
			<>
				<style>{`.${className} {${style}}`}</style>	
				<h1 className={className}>{children}</h1> 
			</> 
		 );
	}
	return Component;
}

const backgroundColor = 'black';
const StyledH1 =  h1`
	background-color: ${backgroundColor};
	color: pink;
`;

function App() {
	return <StyledH1>Hello World</StyledH1>;
}

export default App;
```

마지막으로 함수를 삽입하는 예시
```jsx
function h1(strings, ...values) {
  // React 컴포넌트를 만든다
  function Component({ children, ...props }) {
    // 템플릿 리터럴에서 받은 값을 CSS 코드로 만든다
    let style = '';
    for (let i = 0; i < strings.length; ++i) {
      style += strings[i];
      // 삽입된 값이 함수이면 props를 가지고 실행한 값을 CSS에 넣는다.
      if (typeof values[i] === 'function') {
        const fn = values[i];
        style += fn(props);

        // 그 외에 값이 존재하면 CSS에 문자열로 넣는다.
      } else if (values[i]) {
        style += values[i];
      }
    }

    // CSS 코드에 따라 클래스 이름을 만든다
    const className = `my-sc-${style.length}`;

    // `<style>` 태그로 만든 CSS 코드를 렌더링한다
    return (
      <>
        <style>{`.${className} {${style}}`}</style>
        <h1 className={className}>{children}</h1>
      </>
    );
  }
  return Component;
}

const backgroundColor = 'black';
const StyledH1 = h1`
  color: pink;
  ${({ dark }) => dark && 'background-color: black;'}
`;

function App() {
  return <StyledH1 dark>Hello World</StyledH1>;
}

export default App;

```
1. template literal로 태그 함수 h1을 실행해서,  StyledH1 이라는 컴포넌트가 만들어진다.
2. App컴포넌트를 렌더링하면 StyledH1 컴포넌트도 렌더링한다.
3. StyledH1 컴포넌트에서는 CSS코드를 생성해서 `<style>` 태그로 넣는다. 이때 함수로 삽입된 값(`${({ dark }) => dark &&  'background-color: black;`} ) 부분은 함수이기에 , Props를 가지고 실행해서 CSS 로 만든다.
4. 위 코드에  dark값이 있기에 CSS에서는 `background-color: black;` 이 라는  값으로 반영된다.