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
const {data: postsDataByUsername } = useQuery({
	queryKey: ['posts', username, {status: private}]
	queryFn: () => postsDataByUsername(username);
});
```
아규 먼트로 전달해줘야하는  상황일때는 queryFn으로 화살표함수를 만들어주면된다.
queryFn은 Promise를 리턴하는 상황에서는 어떤 형태의 함수도 상관없다.

쿼리키에 있는값을  아규먼트로 전달하고 싶다면 username이라는 값을  이용하고 싶으면  배열의 1번 인덱스 요소를 아규먼트로 넣어주면된다.
```js
queryKey ['posts', username],
queryFn: () => postsDataByUsername(queryKey[1]);
```
```js
// 혹은 다음과 같이 쿼리 키에서 객체의 특정한 값을 가져와 활용가능
const username = 'codeit';
const {data: ...} = useQuery({
	queryKey: ['posts',{username}],
	queryFn: ({queryKey}) => {
		const [key, { username }] = queryKey;
		return ...(username)	
	}
})

```
순서에  상관없이 같은  값들을 가지고 있는 개체라면 같은  쿼리로 인식하지만, 배열을 쿼리 키로 전달하면 요소의 순서가 중요하다.
즉 배열의 요소로 쿼리 키를 "지정"시 순서에 유의해야한다.
```js
// 다음 세 가지는 모두 같은 쿼리로 인식한다
useQuery({ queryKey: ['posts', { username, userEmail }], ... });
useQuery({ queryKey: ['posts', { userEmail, username }], ... });
useQuery({ queryKey: ['posts', { userEmail, username, other: undefined }], ... });

// 다음 세 가지는 모두 다른 쿼리로 인식한다
useQuery({ queryKey: ['posts', username, userEmail], ... });
useQuery({ queryKey: ['posts', userEmail, username], ... });
useQuery({ queryKey: ['posts', undefined, userEmail, username], ... });

```