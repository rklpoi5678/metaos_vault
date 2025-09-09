## useQuery로 데이터 받아오기

**쿼리란?**
백엔드로부터 데이터를 받아오기  위해 리액트 쿼리에서 제공하는 `useQuery()`훅을 사용. 여기서 쿼리란 '문의하다,질문하다' 라는 뜻을 가지고 있음, 데이터베이스에서 우리가 필요한 데이터를 요청하는것
useQuery() 는 필요한 데이터를  백엔드에  요청해서 받아오는 ReactHook

**useQuery()**
api.js
```js
export async function getPosts(){
	const response = await fetch(`${BASEURL}/posts`);
	return await response.json()
}
```

homepage.tsx
```tsx
import { useQuery } from '@tanstack/react-query';
import { getPosts } from './api/api';

function HomePage() {
	const posts = useQuery({ queryKey: ['posts'], queryFn: getPosts}) 
	console.log(posts);
	
	return <div>홈페이지</div>
} 

export default function HomePage;
```

**useQuery()리턴값 살펴보기**
![[Pasted image 20250909133223.png]]

데이터
data는 우리가 받아온 벡엔드 데이터들이 들어있다. 리스폰스 바디로 받은 데이터가 객체로 되어있고, 페이지네이션에 필요한 정보들과 함께 results란 항목에 실제 포스트 데이터가 배열로 들어아가있다.

데이터를 받아온 시간
 dataUpdatedAt이라는 항목. 현재의 데이터를 받아온 시간을 나타내는항목. 이사간을  기준으로 언제 데이터를  refetch할 것인지를 정한다.

다양한 상태 정보
`isError,isFetched,isPending,isPaused,isSuccess`와 같은 다양한 상태 정보도 확인해볼수있다. status라는 항목에는 success라고 적혀있는데 데이터를 성공적으로 받아왔다는 뜻이다.

## Query Status와 Fetch Status
리액트 쿼리의 두가지상태이다.
Query Status는 실제로 받아 온  data 값이  있는지 없는지를 나타내는 상태값이다.
fetch  status는 queryFn() 함수가 현재 실행되는 중인지 아닌지를 나타내는 상태값이다.

Query Status는 status값을 통해 확인
Fetch Status는 fetchStatus값을 통해 확인가능

**Query Status**
3 가지 상태를 가짐 `pending, success, error`의 상태값중 하나를 가지게됨
펜딩은 아직 데이터를 가져오지 못했을때
에러는 데이터 받아오는 중 에러가 발생
성공은 말그대로 성공

처음 DOM트리에 마운트되고 useQuery()가 실행되면서, 데이터를 아직 받아오기 전이므로 펜딩상태
그 후찍히는 콘솔은 에러나 성공이 찍히면서 데이터가 나오게됨

**Fetch Status**
3 가지상태  `fetching, paused, idle`  현재 쿼리 함수가 실행되는 중일 때에는 패칭상태가된다. 시작은 했는데 실행되지 않다면 퍼즈상태 (오프라인이 된경우 fetch status가 퍼즈상태가 된다.)
idle은 쿼리  함수가 어떤 작업도 하지 않고 있는 상황 (fetching, paused 상태도 아닐경우)
![[Pasted image 20250909143346.png]]
> fetch status는 데이터를 성공적으로 가져왔는지 여부에 상관없이, 쿼리 함수의 실행이끝나면  idle 상태가 되고 이후 서버에서 다시 받아오는 refetch 작업이 발생하면 쿼리 함수가 재실행되어  fetching으로 가게됨

이처럼 2가지 상태조합으로 다양한 상태가 되는에 다양한 상황에  맞춰 디테일한 구현이 가능합니다.