## 글로벌 스타일
```jsx
* {
  box-sizing: border-box;
}

body {
  font-family: 'Noto Sans KR', sans-serif;
}
```
모든 컴포넌트에 적용하고 싶은 코드가 생기는 경우가 있다.  css 함수를 사용해서 변수를 만들고  사용할 수도 있겠지만 모든 컴포넌트에 일일이 값을 넣어주는 건 너무 귀찮은 일이다.
```jsx
import { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`
	* {
	  box-sizing: border-box;
	}
	
	body {
		font-family: 'Noto Sans KR', sans-serif;	
	}
`;

function App() {
	return(
		<>
			<GlobalStyle />
			<div>글로벌 스타일</div>	
		</>
	);
}

export default App;
```

## 애니메이션
과거에는 애니메이션을 만들때 프레임 각각을 모두 만들었지만, 요즘에는 움직임의 기준이 되는 프레임만 만들고 그 사이의 프레임들을 자동으로 채워 넣는 방식을  주로 사용한다. 이때 '움직임의 기준이 되는 프레임'을 '키프레임'이라고 부릅니다.

```jsx
<div class="ball"></div>

@keyframs bounce {
	0% {
		transform: translateY(0%);	
	}
}

.ball {
	animation: bounce 1s infinite;
	...
}
```
> 키프레임 애니메이션을 선언한 다음에, 그걸 animation속성에서 이름으로 쓰고 있다.


```jsx
import styled, { keyframes } from 'styled-components';

const placeholderGlow = keyframes`
  50% {
    opacity: 0.2;
  }
`;

export const PlaceholderItem = styled.div`
  background-color: #888888;
  height: 20px;
  margin: 8px 0;
`;

const Placeholder = styled.div`
  animation: ${placeholderGlow} 2s ease-in-out infinite;
`;

export default Placeholder;
```
```jsx
import styled from 'styled-components';
import Placeholder, { PlaceholderItem } from './Placeholder';

const A = styled(PlaceholderItem)`
  width: 60px;
  height: 60px;
  border-radius: 50%;
`;

const B = styled(PlaceholderItem)`
  width: 400px;
`;

const C = styled(PlaceholderItem)`
  width: 200px;
`;

function App() {
  return (
    <div>
      <Placeholder>
        <A />
        <B />
        <C />
      </Placeholder>
    </div>
  );
}

export default App;
```
```json

// 함수가 리턴하는 변수는 단순한 문자열이 아니라 JS Object 이다.
// 리턴되는  값이 이런 객체이기 때문에 반드시 styled함수나 css함수를 통해 사용해야 ㅎ 나다는 것을  주의해야한다.
{
    id: "sc-keyframes-bEnYbJ"
    inject: ƒ (e, t)
    name: "bEnYbJ"
    rules: "\n  50% {\n    opacity: 0.2;\n  }\n"
    toString: ƒ ()
}
```

##  테마
 ThemeProvider로 테마 설정 사용하기
 Context사용, Styled Components에서도 Context를 기반으로 테마를 사용할 수 있습니다.
 ```jsx
 import { ThemeProvider } from "styled-components";
import Button from "./Button";

function App() {
  const theme = {
    primaryColor: '#1da1f2',
  };

// ThemeProvider Context Provider를 이용해서 theme이라는 객체를 내려준다. 컴포넌트에서는 Props를 사용하듯이 theme이라는 객체를 쓸수있다.
  return (
    <ThemeProvider theme={theme}>
      <Button>확인</Button>
    </ThemeProvider>
  );
}

export default App;

 ```
 ---
 ```jsx
 // 프롭 값을 사용하듯이 theme이라는 값을 쓰고, 기존에 있던 배경색 대신에 아래처럼 함수를 삽입해서 테마 값을 사용한다.
 const Button = styled.button`
	background-color: ${({ theme }) => theme.primaryColor };
 `
 
 ///////////////////////////////////////////////////////////////////
 //// 여러 테마를 선택하게 하고 싶다면 useState를 활용해서 테마를 바꿔준다./////
 ///////////////////////////////////////////////////////////////////
 
import { useState } from 'react';
import { ThemeProvider } from 'styled-components';
import Button from './Button';

function App() {
  const [theme, setTheme] = useState({
    primaryColor: '#1da1f2',
  });

  const handleColorChange = (e) => {
    setTheme((prevTheme) => ({
      ...prevTheme,
      primaryColor: e.target.value,
    }));
  };

  return (
    <ThemeProvider theme={theme}>
      <select value={theme.primaryColor} onChange={handleColorChange}>
        <option value="#1da1f2">blue</option>
        <option value="#ffa800">yellow</option>
        <option value="#f5005c">red</option>
      </select>
      <br />
      <br />
      <Button>확인</Button>
    </ThemeProvider>
  );
}

export default App;

 ```
 
 ## 상황별 유용한 팁
**버튼 모양 링크가 필요할 때**
반복되는 스타일링 코드를 어떻게 관리할까? -> 간편하게 사용할 수 있는게 바로 as라는 Prop입니다. 아래와 같이 버튼이라는 컴포넌트가 버튼 태그로 만들어져 있을 때, 이걸 a 태그로 바꿔서 사용할 수 있습니다.
```jsx
const Button = styled.button`
	/* ... */
`;
```
as로 태그이름을  내려주면 해당하는 태그로 사용할수있다. 굳이 버튼 모양의 링크 컴포넌트를 만들 필요가 없어진다.
```jsx
<Button href="..."  as="a">
	LinkButton
</Button>
```

**원치 않는 Props가 전달될 때**
```jsx
import styled from 'styled-components';

function Link({ className, children, ...props }) {
  return (
    <a {...props} className={className}>
      {children}
    </a>
  );
};

const StyledLink = styled(Link)`
  text-decoration: ${({ underline }) => underline ? `underline` : `none`};
`;

function App() {
  return (
    <StyledLink underline={false} href="https://codeit.kr">
      Codeit으로 가기
    </StyledLink>
  );
}

export default App;
```
> a  태그에는 underline 속성을 지정했는데, 그 속성의 값이  문자열이 아니라 생긴 오류이다. 근본원인은 `<a {...props} className={className}>`이 부분이다. 스프레드를 하는 과정에서 의도하지 않은  언더리인 프롭까지 내려간 것이 원인이다.

1. StyledLink 컴포넌트에서 underline이라는 프롭을 받는다.
2. StyledLink가 스타일링하고 있는 Link컴포넌트에 underline 프롭이 전달된다.
3.  Link 컴포넌트에서 스프레드 문법을 통해 a태그에 underline 프롭이 전달된다.
즉 이럴때 구조 분해 코드를  조금 고쳐 underline을  제외하면 원치 않는 Prop이 전달되는 것을 막을 수있습니다.
```jsx
// 프롭은 링크가 아니라 StyledLink컴포넌트에서만 쓰려고 만든것데 링크에  프롭으로 전달되는게 좀 더 근본적인 문제인 거같습니다.
function Link({ className, children, underline,  ...props }) {
	return (
		<a {...props} className={className}>
			{children}	
		</a>
	);
};

// 아예 프롭이 전달하지않게 하는것이 있는데, Transient Prop 이라는 것을 사용( Transient는 일시적인,순간적인 이라는 뜻이다.)
// Transient Prop을 만들려면 앞에서 $기호를 붙여주면 된다. $underline Prop은 StyledLink안에서만 사용되고, Link로 전달되지않는다.
import styled from 'styled-components';

function Link({ className, children, ...props }) {
  return (
    <a {...props} className={className}>
      {children}
    </a>
  );
};

const StyledLink = styled(Link)`
## 프롭에 $사용
  text-decoration: ${({ $underline }) => $underline ? `underline` : `none`};
`;

function App() {
  return (
  //프롭에 $사용
    <StyledLink $underline={false} href="https://codeit.kr">
      Codeit으로 가기
    </StyledLink>
  );
}

export default App;

```