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
-> stale tiem이 지났는지 아닌지에 상관없이 무조건 stale상태로 만들고,  해당 데이터를 백그라운ㄷ