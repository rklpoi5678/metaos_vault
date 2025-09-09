## 이벤트  핸들러
```tsx
import {... , ChangeEvent , MouseEvent} from 'react'

// 그냥 Evnet에 ChangeEvent를 넣으면 타겟 타입이 추론하지 못하니 제네릭을 넣는다.
// 구체적으로 타입을  명시하고 싶으면  제네릭을 사용한다.(추천)
function handleChange(e: ChangeEvent<HTMLInputElement>) {
}

// 만약 버튼이벤트에 아무런 기능이없고 필요가없다싶으면 이렇게 하는것도 좋지만 
function handleClick(e: MouseEvent<HTMLMouseElement>) {
}

// react에서 제공하는 SyntheticEvent도 있다. UI관련해서  조상격인 타입이다.
function handleClick(e: SyntheticEvent) {
}
```
## Context
```tsx
import { createContext, useContext, useState } from 'react';

type Locale = en |  
```