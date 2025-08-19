## require vs import
로컬 모듈(자신이 작성한 모듈)과 서드파티 모듈을 import하는 방식이 통일되어야 하기 때문에 requre()을 import로 바꿔서 사용하는것을 추천한다.

## package.json
모듈을 패키지로 부르니까 package로 불리었다.
```json
{
	"dependencies": {
		"date-fns": "^2.30.0"
	}
}
```
> dependencies는 서드파티 패키지들의 목록을보여준다.