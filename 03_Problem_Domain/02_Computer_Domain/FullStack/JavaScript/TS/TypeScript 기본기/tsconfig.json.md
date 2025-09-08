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