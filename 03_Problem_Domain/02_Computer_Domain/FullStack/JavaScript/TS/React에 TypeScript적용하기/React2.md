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

type Locale = 'en' | 'ko'

interface LocaleContextValue = {
	Locale: Locale;
	setLocale: (value: Locale) => void;
}

const LocaleContext = createContext<LocaleContextValue>({
	locale: 'ko',
	setLocale: () => {},
})
```

```tsx
export function useTranslate() {
	const locale = useLocale();
	const t = (key: keyof typeof dict[Locale])  => dict[locale][key]
	return t;
}
```
## 타입스크립트에서 파일을 import하는 경우
Create React App기준 CSS 파일이나 이미지 파일같은것을 사용하는데, 미리 세팅해둔 타입 정의가 있기 때문이다.
```
// react-app-env.d.ts
/// <reference type="react-scripts" />
```
>  create react app 에서  만들어 ㄴ 호은  타입 정의 파일을 불러오는  코드이다.

**CSS 파일을 위한 타입들**
css 에서  임포트하는 문법을 쓰려면 문제가 생긴다.  자바스크립트 파일도 아니고, 타입스크립트 파일도 아니기 떄문에 불러온 변수의 타입을 알 수 없기 때문이다. 그래서 이런 경우엔  d.ts파일을 만들어서 타입을 정의해준다.

`declare module` 문법은 모듈의 타입을 직접 정의하는 문법이다.
```tsx
import styles from './Button.module.css';

function Button({ children }) {
	// 실제로 사용하는 경우
	return <button className={styles.Button}>{ children }</button>
}
```

```tsx
declare module  '*.module.css' {
	const classes:  { readonly [key: string]: string}
	export default classes;
}

declare module  '*.module.scss' {
	const classes:  { readonly [key: string]: string}
	export default classes;
}

declare module  '*.module.sass' {
	const classes:  { readonly [key: string]: string}
	export default classes;
}
```
실제 CSS 파일의 처리는 번들러에서 해주지만, 타입스크립트에서는 CSS모듈의 타입을 추론할 수 없기때문에 타입 정의를 직접 해줘야 합니다. 타입 정의만 있으면 무조건 CSS 파일을 쓸 수 있는 건 아니고, 번들러의 설정이 필요합니다. 이 부분은 Create React App이나 Vite, Next.js 같은 것들이 대신해 주고 있습니다.

**이미지 파일을 위한 타입들**
```ts
declare module '*.bmp' {
  const src: string;
  export default src;
}

declare module '*.gif' {
  const src: string;
  export default src;
}

declare module '*.jpg' {
  const src: string;
  export default src;
}

declare module '*.jpeg' {
  const src: string;
  export default src;
}

declare module '*.png' {
  const src: string;
  export default src;
}
...

```
next.js에서 이미지를 불러오면 객체 타입인데.  StaticImageData라는 타입으로 정의 물론 실제로 import했을 때 처리하는 건  Next.js에서 내부적으로 구현된 기능들일 것이다. 타입은 어디까지나  타입일 뿐이다.
```ts
declare module '*.jpg' {
  const content: import('../dist/shared/lib/image-external').StaticImageData

  export default content
}

declare module '*.jpeg' {
  const content: import('../dist/shared/lib/image-external').StaticImageData

  export default content
}

```

## 정리
htmltype
HTMLElement Type
```tsx
const usernameInput = document.getElementById('username') as HTMLInputElement;
const submitButton = document.getELementById('submit') as HTMLButtonElement;
```
event type
기본적으로 Event타입을 쓸수있고 구체적으로는  ~Event로 끝나는 타입을 활용하면 된다.