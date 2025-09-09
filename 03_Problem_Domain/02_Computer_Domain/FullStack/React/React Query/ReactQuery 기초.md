## useQuery로 데이터 받아오기

**쿼리란?**
백엔드로부터 데이터를 받아오기  위해 리액트 쿼리에서 제공하는 `useQuery()`훅을 사용. 여기서 쿼리란 '문의하다,질문하다' 라는 뜻을 가지고 있음, 데이터베이스에서 우리가 필요한 데이터를 요청하는것
useQuery() 는 필요한 데이터를  백엔드에  요청해서 받아오는 ReactHook

**useQuery()**
api.js
```tsx
import { useQuery } from  '@tanstack/react-query';

export async function getPosts(){
	const response = await fetch(`${BASEURL}/posts`);
	
	return await response.json()
}

```