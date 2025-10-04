
![[Pasted image 20251004213016.png]]
> 보통 회원가입 이나 로그인이 되었으면 리다이렉트 시켜준다.(다시 돌아가면 안되니)
> withCredentials: true : 쿠키를 받고 보내고 할때 이러한 옵션이 필요하다.

## 리퀘스트에서 쿠키 사용하기
**Origin이란?**: 리퀘스트를 보내는 사이트의 도메인이다.
http://localhost:3000 에서 https://learn.codeit.kr 로 리퀘스트를 보내는 경우, 서로  다른 오리진  이라 는 의미에서 Cross Origin이라고 표현한다. 여러 가지 보안문제 때문에 특별히 주의

**Credential이란?**: 자격,증명서이다. 웹 개발에서 크래덴셜이란 유저를 증명할 수 있는 정보들을 말한다. 아이디와 비번이라던지 서버에서 발급받은 토큰 같은 것들을 말한다. 리퀘스트를 보내는 상황에서는 주로 쿠키를 말한다.

**Axios에서 Credential사용하기**
withCredentials라는 옵션을 불린형으로 지정할 수 있다. 이 값을  트루로 설정해야만 Cross Origin에 쿠키를 보내거나 받을 수 있다. 이건 패치 함수에서  credentials: 'include'를  설정하는 것과 같다.
```js
axios.post(
	'/auth/login',
	{ email: 'email@email.kr', password: 't3st!'},
	{ withCredentials: true},
)
```
`fetch()`함수에서 Credential
- omit : 쿠키를 사용하지않는다. 리퀘 쿠키사용안하고 리스 헤더를 받아도 저장하지않는다.
- same-origin: 기본값이다. 같은 오리진일 경우에만 쿠키를 사용하겠다. 프론트,백엔드 서버의 주소가 다르다면 Cross Origin이라고 이해한다.
- include: Cross Origin인 경우에도 쿠키를 사용한다.
> 프론트 사이트 와 다른 오리진일 경우 CORS에서 쿠키를 사용하려면 credentials: 'include'를 설정해야한다는점이다.
>> 실제 개발을  백엔드 서버와 같은 오리진에서 진행한다면 굳이 설정하지않아도 기본값이 적용된다.
```js
fetch('https://learn.codeit.kr/api/link-service/auth/login), {
	method: 'POST',
	headers: { 'Content-Type': 'application/json' },
	body: JSON.stringify({ email: 'email@email.kr', password: 't3st!' }),	
	credentials: 'include'
});
```

## 쿠키가 제대로  저장되지 않을 때

1. res header의 set-cookie 체크하기
	1. 네트워크 텝에서 리스폰스 헤더확인 안에 쿠기확인
	2. `에러메시지: This attempt to set a cookie via a Set-Cookie header was blocked because it had the "SameSite=Strict" attribute but came from a cross-site response which was not the response to a top-level navigation.
	3. Cookies탭을 사용하면 표 형태로 좀 더 편리하게 사용할수있다.
	4. ![[Pasted image 20251004214543.png]]

2. SameSite Option
	1. 리퀘스트를 보내는 쪽의 도메인과 리퀘스트를 받는 쪽의 도메인이  일치하는지 확인 후 쿠키의 사용을  허용하는 옵션이다. 이런 옵션은 백엔드 쪽에서  설정한다.
	2. 좀더 엄격한 규칙으로는 SameSite-Strict옵션이 있는데, 반드시 req와 req를 받는 쪽이 같은 도메인이어야 저장하고 사용할수있다.

원인을 찾았다면
개발자  도구에서 리퀘스트 헤더와 리스폰스 헤더를 복사해서 백엔드 개발자에게 확인을 요청한다.

## 항상 Access Token 사용하기
![[Pasted image 20251004215552.png]]`
> 매번 withCredentials를 사용하지않아도된다. constants나 lib에 공통으로 사용하는 것을 넣는다.axios
> 

## 컨텍스트 유저 데이터 관리하기 2
유저데이터는 전역적으로 사용하니 컨텍스트로 활용하는편이다.

[[React 유저 기능 구현하기 2]]