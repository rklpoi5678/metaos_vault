## 함수형
- 변환, 이벤트 처리, 상태 업테이트 등
- 함수의 조합으로 잘게  나누고,, 부수효과를 최소화할때 강점이있다.
- react hook, 배열/컬렉션 데이터 처리(map,filter,reduce)
## 객체지향(OOP)
- 복잡한 상태와 동작을 한 덩어리로 묶어서 추상화할 때 강점
- 도메인 모델, 게임 엔진, GUI 시스템, 대규모 엔터프라이즈 서비스 등
- 클래스 기반 서비스 계층, 디자인 패턴(Factory,  Observe 등)

도메인로직은 객체지향, 유틸리티-데이터  파이프라인은 함수형
게임개발/임베디드:  여전히 OOP중심, 패턴으로 구조화
한쪽만 고집하지않고, 문제 특성에 맞는  접근을 한다. 두 스타일의 장 단점을 이해하고 필요하면 섞는다.
팀원과 코드의 유지보수를 고려해서 스타일을 정한다.

## 엔트리포인트(zod 패키지의 index.ts)
**외부 모듈의 내용을 다양한 형태로 다시 내보내는 ( re-export)패턴이다.**
```js
import * as z from "./v4/classic/external.js"
```
-  해당 external에안 모든export를  하나의 네임스페이스 객체 `z`를 가져온다.
- 즉 `z.string,z.number,z.object` ...이런 식으로 접근 가능
```js
export * from "./v4/classic/external.js"
```
- 원래 그 모듈이   export하던 모든 심볼을 이 파일에서도 그대로 export (통과한다는 느낌)
- 그래서 `import {string} from '이모듈'`처럼 불러오는게 가능
```js
export { z };
```
- 네임스페이스 (as z ) 자체를 이름있는  export로 노출시킨다.
- 이렇게 하면 사용하는쪽이 ( 주는것)
```js
import { z } from '이모듈(index.ts에서 내보냄)';
z.string(...);
```

```js
export default z;
```
> z 를 기본(default) export로도 내보냄

이렇게 하면 사용하는 쪽
```js
import z from "이모듈(index.ts에서 내보냄)"
```