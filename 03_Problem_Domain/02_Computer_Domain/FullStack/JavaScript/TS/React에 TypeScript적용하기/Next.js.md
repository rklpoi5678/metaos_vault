## Pages Router타입
커스텀 app
```app.tsx
AppProps라는 타입을 next/app패키지에서 불러와서 아래처럼사용
import { AppProps } from 'next/app'

export default function App ({ Component, pageProps }: AppProps) {
	// ....
}
```

## 프리렌더링
빌드  시점에 리엑트 코드를 미리 렌더링해 둘수있다. 이런 것을 정적생성(Static  Generation)
