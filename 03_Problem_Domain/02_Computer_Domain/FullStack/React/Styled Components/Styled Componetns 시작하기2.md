## 다이내믹 스타일링
```jsx
import styled  from 'styled-components';

const SIZES = {
	large:  24,
	medium: 20,
	smail: 16,
}

const Button = styled.button` 
	background-color: #6750a4; 
	border: none; 
	border-radius: ${({ round }) => round ? `9999px` : `3px`}; 
	color: #ffffff; 
	font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px; 
	padding: 16px; 
	
	&:hover, 
	&:active { 
		background-color: #463770; 
	} 
`; 

export default Button;

// App.jsx
import styled from 'styled-components';
import Button from './Button';

const Container = styled.div`
  ${Button} {
    margin: 10px;
  }
`;

function App() {
  return (
    <Container>
      <h1>기본 버튼</h1>
      <Button size="small">small</Button>
      <Button size="medium">medium</Button>
      <Button size="large">large</Button>
      <h1>둥근 버튼</h1>
      <Button size="small" round>
        round small
      </Button>
      <Button size="medium" round>
        round medium
      </Button>
      <Button size="large" round>
        round large
      </Button>
    </Container>
  );
}

export default App;

```
이런식으로 자바스크립트 코드를 집어넣을수있따. 이것을 표현식 삽입법(Expression Interpolation)이라고 부르는데 JSX에서 Prop나  State에 따라 HTML 태그를 다르게 보여주는 것과 비슷하다.

## ${...} 안에 함수 사용하기
함수의  파라미터로 Props를 받고, 리턴 값으로는 스타일 코드를  리턴해주면된다. 이건 템플릿 리터럴의 기능이 아니라 Styled Components가 내부적으로 처리해주는것o