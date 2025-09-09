## useMutation으로 데이터 추가하기
뮤테이션은 '형태나 구조상의 변화' 여기서 뮤테이션이란 사이드 이펙트를 가진 함수를 의미한다.
데이터베이스의 새로운 값을  추가하거나 삭제,수정하는 행위는 사이드 이펙트에 해당한다. 이렇게 사이드 이펙트가 발생한경우 useMutation()을 사용한다.

useMutaion이랑 useQuery차이점 
useQuery의 쿼리 함수는 컴포넌트가 마운트되면서 자동으로 실행
 useMutaion은 실제로 뮤테이션하는 함수를 직접 실행
  mutate() 함수를 통해 mutationFn으로 등록했던 함수를 실행할수있고, 그래야만 백엔드 데이터를 실제로 수정하게됨

뮤테이트를 하면 벡엔드데이터는 변경, 현재 캐시에 저장된 데이터는 리패치하지않고 기존 데이터가 보존 따라서 리패치를 해줘야 변경된 데이터가 화면에 제대로 반영됨

### **useMutaioe()으로 데이터 추가하기**
```js
const uploadPostMutation = useMutation({
  mutationFn: (newPost) => uploadPost(newPost),
});

const handleSubmit = (e) => {
  e.preventDefault();
  const newPost = { username: 'codeit', content };
  uploadPostMutation.mutate(newPost);
  setContent('');
};

```
> 만들어도 데이터가 ui 렌더링이 안됨
> 새로운 데이터를 확인하려면 새로고침

### **invalidateQueries()함수**
이 함수 사용시 업로드가 끝난 이후에 자동으로 리패치를 하도록 설정할 수 있다.
말그대로 모든 쿼리 혹은  특정 쿼리들을 invalidate하는 함수 '무효화하는함수'
-> 캐시에 저장된 쿼리를  무효화한다는 의미
-> stale tiem이 지났는지 아닌지에 상관없이 무조건 stale상태로 만들고,  해당 데이터를 백그라운드에서 refetch하게 된다.

useQueryClient() 훅을 사용해서 가져올 수 있고 원하는 시점에 queryClient.invalidateQuerise()함수를 실행하면 된다.
```js
import { useQueryClient } from '@tanstack/react-query';

const queryClient = useQueryClient();
//...
quertClient.invalidateQueries();
```
> 해당 쿼리를 무효화하면서 데이터를 자동으로 리패치 할 수 있게되고, 그러면 새롭게 업로드된 포스트를 바로 보여줄수있다.

**useMutation() 함수의 콜백 옵션**
언제 무효화를 해야할까
뮤테이션이 성공한 시점에 `['posts']` 쿼리를 무효화해 주는 함수를 콜백으로 등록해 주면 된다. 포스트를  업로드하자마자 업로된 포스트까지 화면에 보이도록할때를 예로
```js
//  `onMutate,onSuccess,onError,onSettled와 같은 주요 옵션들이 있어  뮤테이션 사이클에 따라 적절한 동작을 추가할수있다.`
const queryClient = useQueryClient();
// ...
const uploadPostMutation = useMutation({
	mutatuinFn:  (newpost) => uploadPost(newpost);
	onSuccess: () => {
		queryClient.invalidateQueries({ queryKey: ['posts']})	
	},
});
```

**Mutate() 함수의 콜백 옵션** 
주요 옵션들은 useMutatation()에서도  mutate() 함수에서도 사용가능하다.
이때 useMutation()에 등록한 콜백 함수들이 먼저 실행되고, 그다음에 mutate() 에 등록한 콜백 함수들이 실행됩니다.
```js
const uploadPostMutaion = useMutaion({
	mutaionFn: (newPost) => uploadPost(newPost),
	onSuccess: () => {
		console.log()	
	},
	onSettled: () => {
		console.log()	
	},
});
...
uploadPostMutaion.mutate(newPost, {
	onSuccess: () => {
		console.log():	
	},
	onSettled: () => {
		consoel.log();	
	}
})
```
> useMutaion() 에 등록된 콜백 함수들은 컴포넌트가 언마운트되더라도 실행이 되는데,
> mutate() 에 등록된 콜백 함수들은 무테이션이 끝나기 전 언마운트되면 실행되지않는다.
> -->  뮤테이션 과정에 꼭 필요한 로직은 useMutaion
> --> 리다이렉트, 결과를 토스트를 띄워주는것과 같이 해당 컴포넌트에 종속적이면 mutate()

```js
...

const uploadPostMutation = useMutation({
  mutationFn: (newPost) => uploadPost(newPost),
  onSuccess: () => {
    queryClient.invalidateQueries({ queryKey: ['posts'] });
  },
});

const handleUploadPost = (newPost) => {
  uploadPostMutation.mutate(newPost, {
    onSuccess: () => {
      toast('포스트가 성공적으로 업로드 되었습니다!');
    },
  });
};

```

### **isPending프로퍼티 활용하기**
중복해서 업로드하면  안되니 버튼비활성화
```js
const uploadPostMutaion = useMutation({
	mutationFn: (newPost) => uploadPost(newPost),
	onSuccess: () => {
		queryClient.invalidateQueries({ queryKey: ['posts']})	
	},
});

//...

<button
	disabled={uploadPostMutaion.isPending || !content}
	type='submit'
>
업로드
</button>	
```