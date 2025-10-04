## 로그인 상태에 따라 리다이렉트하기
![[Pasted image 20251004230444.png]]
> useEffect 콜백은 비동기적으로  실행시켜줌, 1번이 먼저 실행되더라도 async 비동기이다.
> 2가 실행되는 시점에서 아직 UserData를 가져오는 시점이니 !user가 트루가되어 로그인페이지로 리다이렉트된다.
![[Pasted image 20251004230608.png]]
유제 데이터를 받는 중과 받기 완료 진리값을 검사하는 코드를 추가하면된다.
이런 코드를 깃발에 비유하여 플래그라고 부른다.

이러한 시점을  잘 생각하고 작성해본다.

## Refresh Token 활용하기
대부분의 경우엔 Access Token 만 전송하도록하고, 이 토큰의 유효기간이 만료되면 Refresh Token을 다시 보내서 최대한 노출을 줄이는 전략을 사용한다.
토큰이 없을때 401에러가 날것이다 캐치로 잡아주면된다.
```js
  async function getMe() {
    setValues((prevValues) => ({
      ...prevValues,
      isPending: true,
    }));
    let nextUser;
    try {
      const res = await axios.get("/users/me");
      nextUser = res.data;
    } catch (error) {
      if (error.response?.status === 401) {
        await axios.post('/auth/token/refresh');
        const res = await axios.get('/users/me');
        nextUser = res.data;
      }
    } finally {
      setValues((prevValues) => ({
        ...prevValues,
        user: nextUser,
        isPending: false,
      }));
    }
  }
```
보통 Interceptors나 미들웨어를 사용한다. (저렇게 계속하면 중복이다.)

interceptors사용
{_retry}를 잘못설정하면 무한루프에 빠질수도있다.
이런게 있다정도로 이해
```js
instance.interceptors.response.use(res => res, async (error) => {
    const originalRequest = error.config;
    if (error.response?.status === 401 && !originalRequest._retry) {
      await instance.post('/auth/token/refresh', undefined, { _retry: true });
      originalRequest._retry = true;
      return instance(originalRequest);
    }
    return Promise.reject(error);
  });
```

## 로그아웃
HttpOnly 옵션떄문에 js로  토큰값을 수정할수없다는것이 걸린다.
그래서 반드시 서버에서 처리해야한다.