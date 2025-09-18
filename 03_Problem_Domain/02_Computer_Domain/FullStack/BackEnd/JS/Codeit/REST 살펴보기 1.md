## URI
좌석은 H열 11번
좌석은 자원이고
H열 11번은 어디좌석인지를 말해주는 식별이다.
웹에서는 이러한 자원의 식별을 URI라고한다.

seat - 단수형
```
// bad
/get-member-list
/create-new-member

// good
/members
/articles
```

seats - 복수형
```
// 여러개의  자원을 반환한다면 복수현, 단 1개 단수형

/members # 멤버 목록(복수형)
/members/1 # 멤버 목록 중, 1번 멤버
/key # 1개의 키
```

seats/h/11 - 식별자 사용
```
// 계츨 표현을 위하여 , 슬새시 사용
/articles
/articles/1
/articles/1/comments
/articles/1/comments/2
```

**마지막  슬래시 붙이지 않기**
트레일링  슬래시라고 하는  마지막 슬래시는 REST에서 어떠한 의미도 가지지 않기 떄문에 혼동을 줄수있다. 따라서 붙이지 않는다.
```
// bad
/artices/1/comments/
// good
/artices/1/comments
```

**모두 소문자로  작성 & 띄어쓰기는 대시 사용**
언더스코어는 가독성을 낮출 수 있기에 사용하지않는다. 띄어쓰기가 필요하다면 대시와 함께 소문자

```
// bad
/artices/1/topVoted
/artices/1/top_voted

// good
/articles/top-voted
```

**파일 확장자 포함하지 않기**
특정 파일을  가리키는지, 아니면 자원의 식별자인지 헷갈릴 수 있기에  넣지 않는다.
Content-Type헤더를 사용해야합니다.

**목록에 필터가 필요한 경우, 쿼리 문자열을 사용**

**URI에 동사 사용하지 않기**
```
// bad
/members/1/delete
/members/2/update

// good
DELETE /members/1
PUT /members/2
```


