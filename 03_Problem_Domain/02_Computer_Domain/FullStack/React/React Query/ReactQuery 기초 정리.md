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
const {data: postsData, isPending, isError} = useQuery({
	queryKey: postsQueryKey,
	queryFn: postsQueryFn,
});

if(!isPending) return 'loading';
if(!isError) return 'isErrorOn';
```

useMutaion사용법
```js
import { ... , useQueryClient } from '@tanstack/react-query';

const queryClient = useQueryClient();

const uploadPostMutaion = useMutaion({
	mutaionFn: (newPost) => uploadFn(newPost),
	onSuccess: () => {
		queryClient.invalidateQueries({ queryKey: ['posts']})	
	}	
});

const handleUploadPost = (newPost) => {
	uploadPostMutaion.mutate(newPost, {
		onSuccess: () => {
			toast('success');	
		},
	});
};
```
DB 값추가 변경시 뮤테이션 훅 활용
useQuery달리 뮤테이션 함수를 실행해서 mutaionFn이 실행
옵션을 통해 각 상황에 맞는 다양한 처리를  할수있다ㅏ.
특히 onSuccess에서  query invalidation 을 통해 자동으로 리패치 가 되도록 할수있다. 이렇게 하면 새로고침을 하지 않아도 새로운 데이터가 화면에 보인다.
