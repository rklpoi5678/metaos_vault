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

## 구글 로그인 구현하기
```js
        <Button
          className={styles.GoogleButton}
          type="button"
          appearance="outline"
          as={Link}
          to="/api/auth/google"
          reloadDocument --  리액트 라우터에서 이동 시키는것이 아니라 실제 get요청을 보낼수있도록 새로고침하는 옵션이다.
        >
          <img src={GoogleImage} alt="Google" />
          구글로 시작하기
```

## 워크플로 이해하기

회원가입
![[Pasted image 20251005001522.png]]
로그인
![[Pasted image 20251005001534.png]]

그후 프론트에서 브라우저저장

세션의 경우 백 - 데이터베이스에서 세션상태를 변경하고 200ok를 프론트에 보내줌

유저데이터  가져오기
![[Pasted image 20251005001548.png]]
GET /users /me 쿠키와 함계 ->  쿠키를 확인하고(백) , 해당 유저 찾기(백-DB), DB에서 유제 데이터를  보내줌 -> 유저데이터를  리스폰스로 보내줌

로그 아웃
![[Pasted image 20251005001607.png]]
Delete /autho/logout -> 쿠키 확인 -> Set-Cookie : 만료된 쿠키를 보내줌
세션의 경우 데이터베이스에서 세션  상태를 변경합니다. -> 200 ok

토큰 갱신하기
![[Pasted image 20251005001558.png]]
인증이 필요한 리퀘스트 -> 실패 -> 상태 코드 401 -> POST / auth/ token/ refresh  -> 토큰 확인 -> 새로운 토큰 생성 -> Set-Cookie: 새로운 토큰으로 리스폰스 해준다.

구글 로그인
![[Pasted image 20251005001626.png]]

이렇게 그린 그림을  시퀀스 다이어그램이라고한다.