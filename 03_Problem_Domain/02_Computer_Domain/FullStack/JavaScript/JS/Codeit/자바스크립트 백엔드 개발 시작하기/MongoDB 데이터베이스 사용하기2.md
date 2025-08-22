## 데이터 생성과 유효성 검사
데이터 생성은 
await Task.create(req.body)
res.status(201).send(newTask);

데이터 유효성 검사는 사용자가 전달하는데이터가 올바른지 확인하는과정이다.
몽구스는 scheam로 추가할수있다.
```js
// 필수 required로 maxLength로 받을수있는 최대길이 설정
// 최대 길이를 초과하면 ValidationErrro가 나온다.
// 몽구스는 스키마에 정의되지 않은 필드는 무시한다.
{
	title: {
		type: String,
		required: true,
		maxLength: 30,
		//validator를 만들어 2단어가 이상이어야 되게만들기
		validate: {
			validator: function(title) {
				return title.split(' ').length > 1;
			},
			message: 'Must contain at least 2 words.',
		},
	},
}
```
