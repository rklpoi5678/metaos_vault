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
 dataUpdatedAt이라는 항목. 현재의 데이터를 받아온 시간을 나타내는항목