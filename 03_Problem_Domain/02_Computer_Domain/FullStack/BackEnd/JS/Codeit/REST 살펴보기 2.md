## 상태 코드
3자리숫자와  상태로표시
```
200 ok
```

## 100번대(정보 응답)

- 100 Continue(계속)
    - 요청의 첫 부분을 받아서 다음 요청을 기다리고 있다는 것을 알려 줍니다.
    - 이미 요청을 완료했다면 해당 응답을 무시할 수 있습니다.

## 200번대(성공 응답)

- 200 OK(성공)
    - 클라이언트의 요청이 성공적으로 처리되었다는 것을 의미하며 주로 요청한 페이지를 서버가 제공했다는 것을 알려줍니다.
- 201 Created(생성됨)
    - 요청이 성공적으로 처리되어 새로운 자원을 생성했다는 걸 의미합니다.
- 204 No Content(콘텐츠 없음)
    - 요청을 성공적으로 처리했으며, 콘텐츠(body)를 제공하지 않는다는 것을 의미합니다.

## 300번대(리다이렉션 메시지)

- 301 Moved Permanently(영구 이동)
    - 요청한 자원이 새로운 위치로 영구 이동했음을 나타냅니다.
    - 클라이언트는 서버가 전달한 리스폰스의 Location 헤더에 작성된 주소로 이동합니다.
- 302 Found(임시 이동)
    - 요청한 자원이 일시적으로 이동했음을 나타냅니다.
    - 클라이언트는 향후 다시 해당 자원을 요청할 때도 동일한 주소로 해야 합니다.
- 304 Not Modified(수정되지 않음)
    - 마지막 요청 이후 요청한 자원은 수정되지 않았다는 것을 알려주며 서버가 콘텐츠를 전달하지 않습니다.
    - 클라이언트는 이전에 전달받은 자원을 계속해서 사용할 수 있습니다.

## 400(클라이언트 에러 응답)

- 400 Bad Request(잘못된 요청)
    - 클라이언트의 요청을 서버가 이해할 수 없음을 의미합니다.
- 401 Unauthorized(권한 없음)
    - 클라이언트가 해당 요청에 대한 응답을 받기 위해서는 추가적인 인증이 필요하다는 것을 의미합니다.
- 403 Forbidden(금지됨)
    - 클라이언트가 요청한 자원에 접근할 권한이 없음을 의미합니다.
    - 401과는 달리 인증된 클라이언트이지만 인가되지 않았음을 의미합니다.
- 404 Not Found(찾을 수 없음)
    - 클라이언트가 요청한 자원을 서버가 찾을 수 없음을 의미합니다.
- 405 Method Not Allowed(메소드 허용되지 않음)
    - 클라이언트가 요청한 HTTP 메소드가 허용되지 않았음을 의미합니다.

## 500(서버 에러 응답)

- 500 Internal Server Error(내부 서버 오류)
    - 서버에서 오류가 발생하여 요청한 작업을 수행할 수 없음을 의미합니다.
- 502 Bad Gateway(잘못된 게이트웨이)
    - 서버가 요청을 처리하는데 필요한 작업을 수행하던 중, 요청을 처리하는 중간 단계의 서버인 게이트웨이로부터 잘못된 응답을 받았음을 의미합니다.
- 503 Service Unavailable(서비스 사용 불가)
    - 서버가 해당 요청을 처리할 준비가 되지 않았음을 의미합니다.
    - 일반적으로 유지 보수를 위해 작동이 중단되거나 과부하가 걸렸을 때 나타나며, 일시적 상황에서 사용됩니다.
- 504 Gateway Timeout(게이트웨이 시간 초과)
    - 서버가 응답을 제한 시간 안에 줄 수 없는 상태임을 의미합니다.

## 미디어 타입과 링크 헤더
Content-type: Media Type
콘텐트타입에는 미디어 타입이 붙었다.(type/subtype)구조로 되어있다.
```
applictation/json, html/text
```
 링크헤더로 문서를 전달하여 해석시킬수있다.
 자기 서술적 메시지는 rest api에서 잘지켜지지않는 조건이기도하다.
 ```http
 HTTP/1.1 200 ok
 Link: <https//exaple.com/docs/codeit-members>; rel="profile"
 {
	"id": 2,
	"name": "Olivia" 
 }
```

## HATEOAS(헤이티어스)
Hypermedia as the engine of application state
하이퍼미디어를 사용한 애플리케이션 상태 표현 및 변경
어떤 페이지로 어떤 행동을 하는지를 알수있어야한다는것이다.

```json
// 헤이티어스를 만족할려면 동작을 지정해줘야한다.
// 리스폰스 바디에 상태 변경을 위한 링크 포함
{
	"id": 2,
	"name": "Olivia" ,
	"delete": {
		"href" :  "member/1",
		"method" : "DELETE"
	}
}
```
**HAL**
```json
{
// 리소스
	"id" : 2,
	"name": "James",
	// 경로 할을 사용하면 리스폰스바디로로 어떻게 해야하는지 표현할수있다.
	"_links": {
		"self": {
			"href": "https://example.com/members/2",
			"method": "GET"	
		}	
	}
}
```
다른 방법은  링크헤더를 이용하는것이다.
```html
<a href="https://asdf..."/>asd</a>
```

## 자주 하는 실수
멤버 목록을 가져오는데 API엔드포인트를 POST를 사용하여 구현한 경우
```http
POST /memebers
```
데이터를 포함하는 엔드포인트를, 겟으로 구현한경우
```http
GET /members?username=harry
```
> 기록되어야 하지 말아야할 정보가 쿼리 스트링을 통해 브라우저 히스토리에 기록이 남을수있다.

**잘못된 상태코드**
 필드의 값을 잘못 전달하여 작업 수행에 실패했지만, 상태코드는 성공인경우
- 멤버 생성 리퀘스트
```http
GET /members

{
	"username": "Harry",
	"age": -10,
}
```
- 새로운 멤버의 생성 실패 리스폰스
```http
200 ok

{
	"error": "age must be grater than 0."
}
```
> 정상적인 리퀘스트로 판단해버릴수있다.

**행동을 나타내는 표현이 포함된 URI**
```
// bad
/create-members
/update-members/1
/delete-members/2
```
```
// good 
POST /members
GET /members/1
DELETE /members/2
```

**누락된  MIME Type**
컨텐츠 타입에 헤더가 없거나 MIME Type 올바르게 지정하지 않으면 서버와 클라이언트가 내용을 잘못 해석할 수 있다. 
- 새로운 멤버의 생성 리퀘새트ㅡ
```http
POST /members
Content-Type: application/json

{
	"name": "Harry"
}
```
- 새로운 멤버의 생성 리스폰스
```
HTTP/1.1 200 ok
content-type: application/json

{
	"id": 2
	"name": "Harry"
}
```
