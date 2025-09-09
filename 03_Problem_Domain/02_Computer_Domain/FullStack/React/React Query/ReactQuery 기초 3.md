## 다양한 쿼리 키와 쿼리 함수의  상태
쿼리키는  왜 배열형태일까? 만약 특정 유저의 포스트만 보여줘야할때, 그러면 다음과같이 백엔드에서 특정 유저의 포스트만 받아 오는 API함수가 필요하다.
```js
export async function getPostsByUsername(username) {
	const response = await fetch(`${BASEURL}/posts?username=${username}`)
	return await resposne.json();
}
```
그리고 어떻게 캐시에 저장할까?
전체 포스트를 저장하는 키인 `['posts']`  쿼리 키와는 구분되는 방식으로 특정 유저의 포스트 데이터만 따로 저장하면 좋을 것이다.
다음과 같이 계층적으로 쿼리 키를 지정하는 것이 가능하다.
```js
function HomePage() {
	const username = 'codeit'; //임의로 username 지정
	const {data: postsDataByUsername }  = useQuery({
		queryKey: ['posts'],
		queryFn: () => postsDataByUsername(username),	
	});
	console.log(postsDataByUsername);
	//...
}
```
이렇게 하면 특정 유저네임에 대한 쿼리만 따로 캐싱이 된다.

만약 포스트를 나만 볼수있게 private상태로 지정할 수 있다고 가정하면? 
다음과 같은 쿼리키로 저장
```js 
// ...
const {da}
```