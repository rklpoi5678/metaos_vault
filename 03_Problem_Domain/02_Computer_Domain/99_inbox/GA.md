## page_view vs screen_view차이점

page_view: 웹페이지 조회수
screen_view: 모바일 페이지 조회수

```js
gtag("event","page_view" {
	page_title
	page_url
})
```

## Click
로그인, 회원가입, 상품 등록등의 버튼을 클릭하였을때 클릭수

event.category: 이벤트 분류(버튼, 링크, 메뉴)
event_label: 이벤트 설명 또는 위치
value: 숫자값(클릭 횟수, 가격등 의미있는 부여가능)

## sign_up
폼에서 받는 값으로 받음 method:email