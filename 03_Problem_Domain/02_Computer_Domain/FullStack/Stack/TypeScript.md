
## 런타임에서 약타입
강타입 언어와 달리 컴파일러는 자바스크립트 즉 본체는 자바스크립트라서 가정을 하고 실행이므로 실행중에는 보장이 안된다.

## 중요
@types/... 처럼 라이브러리에서 타입을 지정해주는 d.ts (tsx)같은 것이 필요하다
자바스크립트만 지원하면 사용이 거의 불가능한편
(타입지정해주는걸 직접만들수있지만 시간이 오래걸림)

### ts-node
기본적으로 TypeScript를 컴퓨터는 바로 이해하지 못한다. Ts->Js 로 변환(컴파일)해야 한다. 그런데 매번 변환하는 과정이 귀찮고 느릴수있다.
> 이 코드를 실행하려면 먼저 변환하고, 그다음 실행해야 해!" 라고 하면 번거롭다

그래서 해결책으로 ts-node라이브러리를 사용한다. TS-> JS로 변환하지 않고 즉시 실행할 수 있게해준다.

#### 작동예제
```Sh
// 일반적인 실행 방식
tsc myfile.ts # TS를 JS로 변환
node myflie.js # 변환된 JS실행
```
```Sh
// ts-node 를 사용하면?
ts-node myfile.ts # 변환 없이 즉시 실행!
```
> TS를 변환하지 않고 즉시 실행할 수 있도록 도와주는 도구이다.
> 개발 속도를 빠르게 하고, 테스트를 쉽게 할 수 있다.

+ 추가로 prisma랑 사용하면 아주 맛있다.

## tsconfig.json

### "moduleResolution"
컴퓨터는 작성한 코드에서 "이 파일을 어디서 가져와야 하지?"라는 질문을 던진다. 예를 들어 import { something } from "libary" 처럼 
그런데 찾는 방식이 여러 가지이면? 어떤 경우는 Node.js 방식으로 찾고, 어떤 경우에는 웹 브라우저 방식으로 찾을수있다.
이걸 결정하는게 moduleResolution 옵션

> TS 가 모듈을 찾는 방법을 결정하는 설정이다. "이 모듈을 어디서 찾을지, 어떤 규치을 따를지"를 정하는 것이다.

#### 작동 예제
```Ts
// Node 방식 (node-modules폴더에서 찾음) import or require()를 사용할때 자동으로 경로 탐색
import { something } from "libray" // node-module에서 찾음
```
```Ts
// Bundler 방식 (웹팩 같은 번들러가 사용하는 방식 ) package.json의 "exports"와"imports"를 지원
import { something} from "library" // 번들러가 최적화된 방식으로 찾음
```
```Ts
// classic  ( typescriptv1.6이전 방식 ) 파일 확장자를 명확히 지정해야 함
import { something} from ".library.ts" // 번들러가 최적화된 방식으로 찾음
```