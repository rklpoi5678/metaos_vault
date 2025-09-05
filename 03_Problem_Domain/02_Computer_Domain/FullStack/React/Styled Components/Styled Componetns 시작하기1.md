## 스타일 컴포넌트란?
리액트 프로젝트에 css적용할때  답답함때문에 만들어졌다. 이러한 불편함 속에서 만들어진것중 가장 인기 있는 기술이 styled Components로 
```jsx
//button
import styled from 'styled-components';

const Button = styled.button`
	background-color: #ededed;
	border: none;
	border-radius: 8px;
`;

function App()  {
	return (
		<div>
			<h1>안녕</h1>		
			<Button>확인</Button>
		</div>	
	);
}

export default App;
```

## 기존 방식의 문제점
**CSS 클래스 이름이 겹치는 문제**
페이스북의 경우 5만개가 넘는 컴포넌트를 사용한다고 하는데 그런 프로젝트에서 겹치지 않는 클래스 이름을 짓는다는것은  거의 불가능에 가깝다
```jsx
const StyledApp = styled.div`
  background-color: #000000;
`;

const Dashboard = styled.div`
  font-size: 16px;
`;

function App() {
  return (
    <StyledApp>
      <Dashboard> ... </Dashboard>
    </StyledApp>
  );
}

```
> 해결법으로 클래스이름을 쓰지 않는 다는것, CSS코드로 리액트 컴포넌트를 바로 만드니까 애초에 클래스 이름이 겹칠 일이 없다.

## 재사용하는 CSS코드를 관리하기 어렵다.
스타일 재사용이 필요한 상황에서 클래스가 아니라 JS변수를 만든다.  JS라 언제 어디서  쓰고 있는지 에디터를 통해 확인하기 쉽고.  이름을 바꾸거나 삭제를  하는 것도  코드 에디터를  통해 쉽게  할 수 있습니다.

## 사용법
```js
import styled from 'styled-components'

// styled.tagname의 tagname부분에는 스타일을 적용할 HTML태그 이름을 쓴다.
// 바로뒤 템플릿 리터럴 문법으로 CSS코드를 적는다. 
const Button = styled.button`
	background-color: #6750a4;
	border: none;
	color: #ffffff;
	padding: 16px;
`;
```

##  Nesting문법
Nesting은 CSS규칙 안에서  CSS 규칙을 만드는 것을 말한다.
앰피던스선택자와 컴포넌트 선택자를 사용
```jsx
import styled from 'styled-componenets';

const Button = styled.button`
	background-color: #6750a4;
	border: none;
	color: #ffffff;
	padding: 16px;
	
	&:hover,
	&:active {
		background-color: #463770;	
	}
`;

export default Button;
```
Nesting에서는 앰피선트는 부모 선택자를 의미한다.

컴포넌트 선택자
```jsx
import styled from 'styled-components';
import nailImg from './nail.png';

const Icon = styled.img`
	width: 16px;
	hight: 16px;
`

const styledButton = styled.button`
	background-color: #6750a4;
	border: none;
	color: #ffffff;
	padding: 16px;

	/* 자손 결합자를 사용할때 앰피선트는 제외해도됨 */
	/* & ${Icon} ===  ${Icon} */
	
	& ${Icon} {
		margin-right: 4px;	
	}
	
	&:hover,
	&:active {
		background-color: #463770;	
	}
`;

/*
아래와 똑같은 효과
	.StyledButton {
		...	
	}
	
	.StyledButton .Icon {
		margin-right: 4px;
	}
*/

function Button({ children, ...buttonProps }) {
	return(
		<styleButton {...buttonProps}> 
			<Icon src={nailing} alt="nail icon" />
			{children}	
		</styleButton>	
	);
}

export default Button;
```
nesting은 여러겹이 가능하기에
```jsx
const styledButton = styled.button`
	background-color: #6750a4;
	border: none;
	color: #ffffff;
	padding: 16px;

	/* 자손 결합자를 사용할때 앰피선트는 제외해도됨 */
	/* & ${Icon} ===  ${Icon} */
	
	& ${Icon} {
		margin-right: 4px;	
	}
	
	&:hover,
	&:active {
		background-color: #463770;	

		/* Nesting된 규칙안에 nesting규칙을 쌓을수있다. */
		${Icon} {
			opacity: 0.2;	
		}
	}
`;

===

.styledButton:hover .Icon,
.styledButton:active .Icon {
	opacity: 0.2;
}
```

