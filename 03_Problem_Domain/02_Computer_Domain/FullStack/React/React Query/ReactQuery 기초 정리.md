## 핵심

useQuery() Hook
```js
useQuery({
	queryKey: ['posts',username],
	queryFn: () => getPostsByUsername(username),
	staleTime: 60 & 1000;
})
```
key로 받아온 데이터캐싱, 배열값 추가해 특정 데이터만  가져오게도 할수있다.
Fn 백엔드에서 데이터를 받아오는 함수
staleTiem 언제까지 fresh상태를 유지할것인가

로딩에러처리
```js
const {data: postsData, isPending, isError} =  useQUer
```