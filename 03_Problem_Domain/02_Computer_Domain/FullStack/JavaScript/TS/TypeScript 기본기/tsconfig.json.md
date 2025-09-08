## 모듈 사용하기
```tsconfig.json
// 기본적으로 트랜스파일링을 하면 같은 소스코드옆에 js가 붙는데 이것을 한폴더에 묶을수있다.
"compilerOptions"{
	"outDir": './dist',
	// rootDir은 기본적으로 컴파일하는 폴더들의 공통조상을 찾아서 그 경로를 기준값으로 한다.  
	// ./ 이런식으로  하면 최상위를 기준으로 dist폴더안에 컴파일된 것들이 들어갈것이다.
	"rootDir": './'
	
},
// 타입스크립트를 설정할때 어떤 파일들을 포함시킬껀지 제외할껀지
// 배열안에 결로를 작성해주면된다.
// "src/**/*" = src폴더안에 모든 폴더 파일들을 포함하겠다는 말이다. 이런 패턴을 글록패턴이라고 한다.
"include": ["src/**/*"],
"exclude"; ["src/test2.ts"]
```

## 자주 사용하는 옵션

**꼭 알아야 할  컴파일러 옵션들**
target: 어떤  ECMAScript 버전으로 변환할지
타입스크립트 코드는 빌드해서 자바스크립트로 변환하는데, 이때 변환할 자바스크립트의 버전을 정할 수 있습니다. 기본적으로 ES7(ES2016)으로 되어있거나함

module: 어떤 방식으로 모듈을 만들지
ESM, CJS방식 
ESM을 쓰려면 es6, es2020같이 es로  시작하는 값을 쓰면 되고, CJS를 쓰려면 commonjs라고 쓰면된다. 프론트엔드 개발시  보통 번들러에서 모듈을 알아서 처리하기 때문에  ESM,CJS상관없을수있다.

exMoudleInterop: ES모듈을 안전하게 사용
import * as moment from 'moment' 라든가  import moment form 'moment'라는 문법은 서로 다른데, 이 옵션을   false로 한다면 CJS로 변환시 두 코드는 같은 형태의 코드로 변환된다. (const moment = require('moment'))

안전하게 모듈을 사용하려면 esModuleInterop옵션은 true로 해놓는 것을 권장한다.

forceConsistentCasingInFileNames: 파일의 대소문자 구분하기
macOS,Window운영체제등  대소문자 구분을 명확하게  하겠다는  옵션, 반드시 true로 해 놓는것을 권장한다.

strict: 엄격한 규칙들 켜기
- noImplicitAny: 아무 타입을 직접 정의하지 않고, 타입 추론도 되지 않는 상태를 implicit any라고 하는데 쉽게 말해 기존 자바스크립트 코드처럼 타입 없이 사용하는 걸 implicit any라고 합니다.
```ts
function printSize(product) {
						~~~~~~ 타입 정의도 없고 추론할 수도 없음
	console.log(product.size);
}
```
기존  자바 스크립트로 만든 프로젝트를 타입스크립트로 옮기는  중이라면 이 옵션을 잠시 끄는 것도 좋다. 
```json
"strict": true,
"noImplicitAny": false,
```
-  strictNullChecks: null이 될 가능성이 있다면  반드시 처리하도록 하는 옵션이다. 되도록  켜놓는것을 추천한다.
```ts
// null로 추론될수있으니 런타임때 오류가날수있다.
let num: number | null;
// ...
num -= 1;
```
- skipLibCheck: 설치한 패키지의 타입 검사하지 않기
node_modules폴더에 설치된 패키지들의 타입검사를 하지 않는 옵션이다. 패키지  개발 과정에서 대부분 타입 검사가 이뤄지기 때문에, 중복으로 하지 않아도된다.

`rootDir`: 최상위 폴더

`outDir`: 자바스크립트 파일을 생성할 폴더
디렉토리 구조에 따라서 자바스크립트 파일을  만듭니다. 값을 지정하지 않을시 소스코드 파일과 같은 폴더에 자바스크립트 파일을 만든다.

- resolveJsonModule: JSON파일 임포트하기
제이슨 파일을 임포트해서 사용하고 싶다면 이 옵션을 켜야 한다.
```js
import data from 'data.json';
//...
```

`include`와`exclude`: tsc로 트랜스파일할 때 포함될 경로와 포함되지 않을 경로를 정해줄수있다. 배열로 경로 패턴을 적어주면된다.

VSCODE에서는 자동완성 기능으로 작성할수있는데, 무엇을 작성해야할지 모를 때 Windows에서는 Ctrl  + I, macOS에서는 Cmd + I 를 입력하면 Suggestion이  뜹니다.
프로젝트를 개발할 떄에는 이기능을 활성하는것을 추천

## tsconfig.json 파일 불러오기
```json
{
	"extends": "<설정 파일 경로>"
}
```

**tsconfig/bases 예시**
tsconfig.json설정을 모아놓은 tsconfig/bases 리포지토리에 있는 설정  파일을 패키지로 설치한 다음, 불러와서 사용
> npm install --save-dev @tsconfig/recommended

```json
{
  "extends": "@tsconfig/recommended/tsconfig.json",
  "compilerOptions": {
  }
}

```
이런식으로 extends옵션을 사용하면 패키지로  설치한 tsconfig.json파일을 불러올 수도 있고,  직접  만든 tsconfig.json 파일을 불러올 수도 있다.'
