##  타입스크립트 설치
 tsc --init
 tsconfig 수정
## 개발 환경 편하게 쓰기
타입스크립트를 위한 노드
노드환경에서 타입스크립트를 곧바로 실행( 자바스크립트 처럼 소스코드를 곧바로 쓸수있게한다.)
```
npm install --save-dev ts-node

package.json
{
  "script" : {
		"dev" : "ts-node src/app.ts" 
  }
}
```
노드몬
```
npm install --save-dev nodemon

package.json
{
// --watch 옵션으로  src폴더를 관찰
// -- exec 옵션으로  ts-node .. 실행
	"script": {
		"dev": "nodemon --watch src  --exec ts-node src/app.ts",	
	}
}

//기본적으로 최신 노드몬은 ts-node에 대해 exec하게 해준다.
 nodemon --watch src src/app.ts
```

## 타입 패키지 설치하기
1. 타입이 공식으로 정의된 파일을  다운받거나
2. 패키지 내부가 자바스크립트만 되어있다면 자신이 직접정의하거나 다른 개발자가 작성한 코드를  다운받으면됩니다.

axios같이 타입스크립트를 자체적으로  지원하는 패키지가 있고(ts로고 존재)
@types/expresss 에 @types같이 타입을 지원하게해주는  패키지가있습니다.

npm 사이트에서 검색하고 찾으면됨

## Express 핸들러  타입 사용하기
![[Pasted image 20251002014753.png]]
이제 타입 정의 가 잘되기때문에 req.만 찍어도 Request타입  객체를 볼수있다. 보통 타입읽기가 쉬운경우  타입안을 참고해서 봐도 되지만, 타입을 읽기힘들정도로 많을경우 보통 밖에서 req. 처럼 점을 찍어 확인할수있다.

타입은 관계이기에 상위 타입인 RequestHander를 이용해서 한번에 타입을 넘겨줄수도있다.
```ts
const handler:RequestHandler = (req,res,next) => {
	res.send();
	req.cookies
};
```
타입을 외울려고하지말고 어떻게 찾아가는지를 알면 어떤 패키지가  와도 능숙하게 쓸수있다.