## React와 TypeScript
```json
// jsx옵션은 jsx를 트랜스컴파일할때 어떤 옵션으로 할것인지를 정하는것이다.
// 즉, 리액트에서  이 확장자들을 어떤방식으로 트랜스컴파일할것인지 정하는것이다.
{
	"compilerOptions": {
	//...
		"jsx": "preserve"	
	}
}
```
tsx는 js로 할건지 jsx를 남겨둘건지 정할수있다. (react,react-jsx규칙을 사용하면 브라우저에 돌아갈수있는 js코드를 만들고  preserve를  하면 별다른 옵션을 안가하고 jsx파일을 남겨놓는다.)
이는 라이브러리들이  어떻게 전략을 구성해서 했냐에따라 다르면 preserve같은 경우 따로 번들로러 js로 바꿔서 트랜스컴파일링을 할때도있다.

next.js 는 JSX를 만들고 자체적으로 처리

## HTML DOM
```ts
const usernameInput = document.getElementById('username')  as HTMLInputElement; //HTMLElement중에서도 input에해당하는 타입이다.

const usernameButton = document.getElementById('submit')  as HTMLButtonElement; //HTMLElement중에서도 input에해당하는 타입이다.

// 이벤트리스너에선 자동으로 타입을 추론해준다.
submitButton.addEventListener("click", function(e) {})

// 간단하게 보편적으로쓰는 Event를 타입으로 명시해줘도 된다 간단하게 만들떄는..
// UIEvent 는 클릭이나 UI에 보편적으로 사용할수있는 타입입니다.
// 실제 자주 사용되는 이벤트는 InputEvent, MouseEvent
// 타입을 명시하면 vscode에서 자동완성기능을 지원해준다.
function handleClick(e: Event) {
	e.preventDefault();
	const message = `${usernameInput.value}님 반갑습니다!`;
	alert(message);
}
```
.d.ts파일은 자바스크립트 없이 타입스크립트로만 타입정의를 모아놓은 파일이다.