
## 코어 커머스 엔진 - 거래 / 결제 / 디지털 전송을 담당
> 중요! 한국 PG(토스, 이니시스, 포트원) 연동 플러그인은 Saleor/Medusa용을 거의 찾을 수 없으니 서버리스 Function으로 PG Webhool<->커머스 API 매핑 방식을 사용하자

### 옵션
Saleor(Python + Django, GraphQL): PWA,Storefront,Admin 별도 제공 GraphQL API 덕분에 프론트 자유도는 높아지며 멀티스토어 버전 관리 내장 다만, 파이선 서버및 한글화 국내 PG 연동 커스텀이 필수로 들어가야한다.

Medusa JS(Node + TypeScript) 플러그인 방식으로 Digital Products레시피 제공 npm기반 확장이 용이하며, Stripe Connect.다중 통화 지원, 다만 발표자료는 많지만 한국 PG모듈 거의 없으므로 직접 제작이 필요한편이다.

## CMS / 상품 메타데이터 계층
Strapi + Digital-Products 플러그인 -> 상품 설명.썸네일.라이선스 태그 관리, 커스텀 빌드(저작권 / 사용 범위) 추가가 쉽다.
Supabase Storage or Cloudflare R2 -> 다운로드 파일을 서명 URL 방식으로 1회성 배포

## 프론트엔드 & 배포
### 스택
- Next.js: SEO.SSR를 챙기면서 Saleor/Medusa GraphQL ro REST SDK를 바로호출
- Tailwind css + shadcn/ui : 상품 Card.필터를 빠르게 조합, LCP 개선
- Vercel or Cloudflare Pages: 글로벌 CDN.Edge Functions로 PG Webhook처리

### 부가 모듈
- 라이선스.다운로드 추적: Medusa "Digital Product Module"예제 + PostgreSQL event log
- Analytics: Plausible / Umami - 쿠키리스 GA 대체, UTM 별 다운로드 추이 파악
- 검색.필터: 알고리아 or Typesense - 카테고리.키워드 실시간 오토컴플릿
- 국내 PG: PortOne(아임포트) Server

> Medusa JS Back + Strapi CMS + Next.js Storefront