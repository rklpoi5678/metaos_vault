## 핵심
클라이언트사이드: HTML안 JS가 돌아가고 JS에 리액트가 돌아가는방식이다.
- 초기 로딩이 느리다.
- 검색 엔진에 제공할 수 있는 정보가 적다
이런 단점을  극복하기위해 프리렌더링(Pre-rendering)이라고한다.
미리 html을 저장해서  보여주거나 ,  서버에서 html먼저 보내는것이다.

Next.js 장점
프리렌더링을 대신해줌, Vercel로 서버 호스팅을 쉽게할수있다.
파일 시스템 기반  라우팅(앱라우팅)을 적용하기에 쉽게 라우팅을 할수있다.

## CSS 적용하기
```jsx
import styles from '../styles/Home.module.css';

export default function Home() {
	return (
		<h1 className={styles.title}>
			Hello Next.js!	
		</h1>	
	)
}
```