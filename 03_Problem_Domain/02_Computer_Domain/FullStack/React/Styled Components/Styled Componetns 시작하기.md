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