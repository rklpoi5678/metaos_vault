## 스타일 재사용: CSS함수
```jsx
import styled from 'styled-components';

const SIZES = {
  large: 24,
  medium: 20,
  small: 16
};

const Button = styled.button`
  ...
  font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px;
`;

const Input = styled.input`
  ...
  font-size: ${({ size }) => SIZES[size] ?? SIZES['medium']}px;
`;
```
중복된 코드가 보인다 이러한 코드를 하나로 합치는것이 바람직할거같다.
```jsx
import styled, { css } from 'styled-components';

const SIZES = {
	large: 24,
	medium: 20,
	small: 16
}

const fontSize = css`
	font-size = ${({size}) => SIZES[size] ?? SIZES['medium']}px;
`

const Button = styled.button`
	...
	${fontSize}
`

const Input = styled.input`
	...
	${fontSize}
`;
```
const boxShadow = `
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
`;
단순한 문자열이라면 일반적인 템플릿 리터럴을 써도 되는데
```jsx
const boxShadow = css`
	box-shaow: 0 5px 15px rgba(0,0,0,0.2);
`;
```
> 이런식으로 css함수를 작성하는것을 습관들이는것이좋다 styled-components를 사용할것이라면