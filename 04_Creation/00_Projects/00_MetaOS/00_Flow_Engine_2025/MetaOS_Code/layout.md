## Next.js 지원 구조 사용

## 전역 디자인 설정 페이지
Next.js 14 이상 버전에서 head.tsx를 안쓰고 metadata로 통합 metadata는 사이트의 타이틀, 설명, 공유지 또는 이름 & 설명, favicon.ico 등을 설정 (=SEO를 위함)

RootLayout은 Children 속성에 들어오는 값들을 전역으로 설정해줄수있음

<ClientWrapper/> [[ClientWrapper]] 컴포넌트 사용