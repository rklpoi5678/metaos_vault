## 핵심
간단한 사이트 경우  React의 state와 props 정도만 활용해도 충분히 만들수있지만, 매우 다양한 데이터가 필요할때 이런 데이터들을  잘관리하고 쉽게  가져다 쓸 방법이 필요하다.
React Context를 사용하면 prop drilling 같은 문제점은 해결할수있었다.

역시 만능이 아니어 보완하기위해 Redux,Recoil등 다양한 상태관리 라이브러리를 이용했다.
데이터는 내  PC에만 사용하는 데이터인 클라이언트 상태 데이터  서버에서 가져온 데이터인 서버 상태  데이터가있다.

앞서 말한 라이브러리들은 클라이언트 상태 데이터들을 잘 관리하기 위해 나온 라이브러리이며, 서버 상태 데이터를 관리하기엔  잘 맞지 않는 부분도 있고, 코드가 복잡해질수도 있다.

이를 해결하기위해  리액트 쿼리가 등장했다.

## 서버 상태(Server State)
데이터 받아오는것에 시간이 걸리기에 비동기식으로 구현된다. 서버 상태데이터는 가능한  최신 데이터를 유지, 데이터를 한번만 받아오는게 아니라 최신 데이터를 가능한 계속받아와야함
사이트에  성격에따라 1초가 중요할수도 있다.

## React Query
데이터를 가져오는 과정에서 로딩과 에러 처리를 쉽게 구현할 수 있도록 여러 값을 제공, 정해진 시간 혹은 조건마다 서버 상태 데이터를 최신으로  가져오는 작업도 알아서 해준다. 
캐시라는 걸 사용해서 매번 서버에서 데이터를 가져올 필요 없이 유저에게 더 빠르게 데이터를 보여주기도함

ReactContext를 배울 때 리액트  Context에서도 데이터를 전역적으로 사용하기 위해 ContextProvide를 사용하듯이, 리액트 쿼리를 사용하려면 쿼리 클라이언트를 제공하는  컨텍스트 프로바이더를  설정해줘야한다.
QueryClientProvider를 통해 쿼리 클라이언트를 제공해 줘야  그 안에 있는 자손 컴포넌트에서 리액트 쿼리를 사용할 수 있게 된다.
```tsx
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import HomePage from './HomePage';

function App() {
	return (
		<QueryClientProvider client={QueryClient}>
			<HomePage />
		</ QueryClientProvider>
	);
}
export default App;
```

**리액트 쿼리 개발자 도구(React Query Devtools)**
> npm install @tanstack/react-query-devtools
```tsx
//...
import { ReactQueryDevtools } from '@tanstack/react-query-devtools';

//...
return (
	//...
	<HomePage />
	<ReactQueryDevtools initialIsOpen={false}/>
)
```
initialopen은 리액트  쿼리 개발자 도구가 열려있는 채로 실행할  것인가를 선택하는 옵션이다.
플로팅버튼을 누르면 개발자 도구처럼뜬다.

