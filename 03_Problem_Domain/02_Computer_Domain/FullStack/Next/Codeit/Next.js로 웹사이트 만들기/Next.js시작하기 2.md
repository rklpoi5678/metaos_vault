## 리다이렉트
만약  옛날 페이지 주소가 products/1인데 바뀌어서 items/1로 변경이되었다면 products에 들어온 사용자의 주소를 변경시켜야된다. 이럴떄  사용하는게 리다이렉트이다.

```js
// next.config.js
// 서버에서 처리할 설정들
/** @type {import('next').NextConfg} */
const nextConfig = {
	reactStrictMode: true,
	async redirects()  {
		return [
			{
				source:  '/product/:id',
				destination: '/items/:id',
				permanent: true,		// 308 permannent redirect 무슨뜻이냐면 브라우저가 리다이렉트 정보를 저장한다.(307과 차이)
			},
		]
	},
}

module.exports = nextConfig

// permanent: false시
statusCode 307 Temporay Redirect

// 우리가 정한 코드 웹 브라우저는 이것을 보고 해당주소로 이동
Location: /item/1
// permanent설정은 기억하기도 어려워서 그떄마다 공식문서에 적용하면된다.
```

## 커스텀 404 페이지
```js
//404.js
import ButtonLink from '@/components/ButtonLink';
import Container from '@/components/Container';
import Header from '@/components/Header';
import styles from '@/styles/NotFound.module.css';

export default function NotFound() {
  return (
    <>
      <Header />
      <Container>
        <div className={styles.notFound}>
          <div className={styles.content}>
            찾을 수 없는 페이지입니다.
            <br />
            요청하신 페이지가 사라졌거나, 잘못된 경로를 이용하셨어요 :)
          </div>
          <ButtonLink className={styles.button} href="/">홈으로 이동</ButtonLink>
        </div>
      </Container>
    </>
  );
} 

```
```css
.notFound {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.content {
  margin: 25px 0 60px;
  text-align: center;
}

.button {
  max-width: 250px;
  width: 100%;
}

```
> 404페이지를 만들면 우리가 직접 404페이지를  꾸며줄수있다.

## 커스텀 APP과 Document
```js
// _app.js
import '@/styles/global.css';

export default function App({ Component, pageProps }) {
	return <Component {...pageProps} />
}
```
> next.js12에서는 공통된 레이어를  구현할때 app.js에 넣으면 된다.

```js
// _document.js
// 여기서는 주로 리액트의 범위를 넘어선 코드를 작성
export default function Document() {
	return (
		<HTML lang="ko">
			<Head />
			<body>
				<Main />
				<NextScript />	
			</body>	
		</Html>	
	)
}
// html의 뼈대를 수정하는 파일
// useState, useEffect 같은 일반적인 컴포넌트 기능을 사용할수없음의 주의!
```
