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

## 스타일  재사용: 상속

styled()함수
```jsx
import styled from 'styled-components';

const SIZES = {
  large: 24,
  medium: 20,
  small: 16,
};

const Button = styled.button`
  background-color: #6750a4;
  border: none;
  color: #ffffff;
  font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px;
  padding: 16px;

  ${({ round }) =>
    round
      ? `
      border-radius: 9999px;
    `
      : `
      border-radius: 3px;
    `}

  &:hover,
  &:active {
    background-color: #463770;
  }
`;

export default Button;
```
```jsx
import styled from 'styled-components';
import Button from './Button';

const SubmitButton = styled(Button)`
  background-color: #de117d;
  display: block;
  margin: 0 auto;
  width: 200px;

  &:hover {
    background-color: #f5070f;
  }
`;

function App() {
  return (
    <div>
      <SubmitButton>계속하기</SubmitButton>
    </div>
  );
}

export default App;

```

## JSX로 직접 만든 컴포넌트에 styled()  사용하기
styled.tagname으로 만든 컴포넌트는 styled()함수에 바로 사용할 수 있지만, 아닌 컴포는 따로 처리가 필요하다.
```jsx
function TermsOfService() {
  return (
    <div>
      <h1>㈜코드잇 서비스 이용약관</h1>
      <p>
        환영합니다.
        <br />
        Codeit이 제공하는 서비스를 이용해주셔서 감사합니다. 서비스를
        이용하시거나 회원으로 가입하실 경우 본 약관에 동의하시게 되므로, 잠시
        시간을 내셔서 주의 깊게 살펴봐 주시기 바랍니다.
      </p>
      <h2>제 1 조 (목적)</h2>
      <p>
        본 약관은 ㈜코드잇이 운영하는 기밀문서 관리 프로그램인 Codeit에서
        제공하는 서비스를 이용함에 있어 이용자의 권리, 의무 및 책임사항을
        규정함을 목적으로 합니다.
      </p>
    </div>
  );
}

export default TermsOfService;
```
```jsx
import styled from 'styled-components';
import Button from './Button';
import TermsOfService from './TermsOfService';

const StyledTermsOfService = styled(TermsOfService)`
  background-color: #ededed;
  border-radius: 8px;
  padding: 16px;
  margin: 40px auto;
  width: 400px;
`;

const SubmitButton = styled(Button)`
  background-color: #de117d;
  display: block;
  margin: 0 auto;
  width: 200px;

  &:hover {
    background-color: #f5070f;
  }
`;

function App() {
  return (
    <div>
      <StyledTermsOfService />
      <SubmitButton>계속하기</SubmitButton>
    </div>
  );
}

export default App;

```
JSX 문법으로 직접 만든 컴포넌트는 styled()함수가 적용될 className에 대한 정보가 없다. styled componenets를 사용하지 않고 직접 만든 컴포넌트는 className값을 prop으로 따로 내려줘야 스타일함수를 적용할수있다.
```jsx
function TermsOfService({ className }) {
	return (
		<div className={className}>
			// ...	
		</div>	
	)
}
```
> styled() 함수가 적용될 부분에 className을 별도로 정해주는 거라고 이해하면도니다. div태그에 클래스를 내려줬기에 TermsOfService안에 있는 div태그에 적용된다.