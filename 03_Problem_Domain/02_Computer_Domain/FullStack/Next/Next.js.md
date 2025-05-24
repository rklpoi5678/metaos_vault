## Next.js 기본 구조

## 개념 설명
Next.js는 React 기반 프레임워크다. 페이지 만들기만 해도 URL로 자동 연결된다. 폴더 구조가 라우팅을 결정한다.

## 왜
React는 SPA이기 때문에 직접 라우팅 코드를 짜야 하는데, Next.js는 자동이라 편하다. SSR, SSG 같은 옵션도 있다.

## Hobby tier(취미티어)
무료 버전의 경우 200개의 프로젝트 까지만 지원 (최대 만들 수 있는 최대 프로젝트 수이다.) 한 Git 저장소 당 연결할 수 있는 프로젝트 수가 제한되어 있으니 연결 방식에 따라선 조금 달라질수있지만 프로젝트 수 자체는 200개 까지 지원

## 예시
- pages/index.js → 홈화면("/")
- pages/about.js → /about 경로 자동 생성
- pages/\[\id\]\.js -> 동적 라우팅

## 다시 설명
Next.js는 React보다 더 ‘사이트 만들기 편한 도구’다. 폴더만 잘 만들어도 페이지가 생긴다.

### 데이터 패칭
### 3.1 `getStaticProps()` - SSG

- **빌드 타임에 한 번만 실행**
- 정적인 페이지 만들 때
```jsx
export async function getStaticProps() {   return { props: { name: "삐삐" } }; }
```


### 3.2 `getServerSideProps()` - SSR

- **요청 올 때마다 실행**
- 사용자 맞춤 데이터 필요할 때

```jsx
export async function getServerSideProps(context) {   return { props: { name: "삐삐" } }; }
```

### 3.3 `API Routes`

- `pages/api/hello.js` → `/api/hello`
- 서버리스 함수처럼 사용

```jsx
export default function handler(req, res) {   res.status(200).json({ message: "Hello 삐삐!" }); }
```

### 스타일링 방식

CSS
```javascript
import styles from './Home.module.css';
<div className={styles.container}></div>
```
<div className={styles.container}></div>
<div className={styles.container}></div>
<div className={styles.container}></div>
Tailwind CSS
```javascript
<div className="bg-black text-white p-4">삐삐 UI</div>
```

### 컴포넌트 구조

Props 전달
```javascript
function Card({ title }) {
  return <h2>{title}</h2>;
}
<Card title="삐삐카드" />

```
동적 라우팅 내부 파싱
```javascript
// pages/blog/[id].js
import { useRouter } from 'next/router';

export default function Post() {
  const router = useRouter();
  const { id } = router.query;
  return <p>블로그 글: {id}</p>;
}

```


#### 파인만 해석(N.E.X.T 독서법)
N - Name: 코드에 이름 붙이기
> **“이건 무슨 역할을 하는 코드지?”**  
>  -> 파일, 함수, 변수, 라우터, useEffect… 전부 역할을 **한 문장으로 정리**


E - Explain: 한 문장으로 설명하기
> “이 줄, 무슨 뜻이야?”  
→ 코드를 **구문 단위로 끊어서 설명**  
→ JSX는 HTML처럼 보여도 **JS 내부 로직**이라는 걸 잊지 말기

X - X-ray: 흐름 분석
>“이 컴포넌트가 호출되면 어떤 일이 일어나?”  
→ **렌더링 순서, useEffect 타이밍, props 전달 경로 등**을 꿰뚫는 훈련

T - Transfer: 내가 쓴다면 어떻게?
>“내 코드에선 이걸 어디 써먹지?”  
→ **내가 직접 똑같은 구조 써보거나**, 지금 보고 있는 웹사이트를 “내가 만든다면?”으로 바꿔 말하기


## Next.js 폴더구조
버전이 13이상일 경우 무조건 app/으로 시작
그 이하일경우(구버전) pages/로 시작

loading.tsx: 데이터 패치가 느릴떄 UX향상을 위해 필수
error.tsx: API나 서버 에러 대응(UX 붕괴 방지)
not-found.tsx: 404 처리 없으면 사용자가 당황하기 떄문에 처리

head.tsx: 검색 최적화(SEO)할때 매우 중요
- 버전 15버전에서는 layout.tsx에서 export const metadata로 설정해야함
- title: 브라우저 제목
- meta name = "description" 구글 검색에 뜨는 페이지 설명
- meta property = "og:image" 링크 공유시 썸네일
- link rel="icon" href="/" favicon.ico
- meta name = "viewport"
- meta charset="utf-8"
- ...

layout.tsx: 전체 구조설정 (서버 컴포넌트여야 해서 'use client'못쓴다는점)
- 따로 ClientWrapper로 자식을 감싸기

## 하이드레이션
렌더링 순서 확실히 한다음 
뷰포인트, whileInVew설정

