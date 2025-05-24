
## 핵심
웹사이트 문앞에 서 있는 "검문관"과 같다. 웹페이지 접속 -> 서버로 요청 -> 요청이 웹페이지로 도달하기 전 middleware라는 작은 코드 조각들이 먼저 실행이됨. 이로 인해 신분증을 확인함

## 기능
특정 사용자가 로그인했는지 확인하거나, 요청한 URL를 다른 곳으로 돌려보내는(redirect)등의 작업을 수행할수 있다. 즉, 요청을 검사하고, 필요하면 수정하거나 거부하는 역할을 한다.

## Next.js의 미들웨어 특징
next에서는 이 미들웨어가 서버 대신 Edge 네트워크(전 세계 분산된 위치들)에서 실행이 된다. 그렇기 때문에 빠르고 효율적으로 요청을 처리할 수있다. 도로 입구에 여러 검문소가 있어서, 어느 곳에 요청이 오든 신속하게 입장을 통제하는 것과 같다고 할 수 있다.

## 사용예시
1. 관리자 페이지: 접근하려는 사용자가 올바른 인증을 받았는지 확인한다.
		사용자가 로그인 상태인지, 인증 토큰이나 쿠키가 있는지 검사하고
		인증되지 않은 사용자는 로그인 페이지로 리다이렉트하는 방식
``` ts
 // middleware.ts (또는 /admin/_middleware.ts)
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  // 예: 인증 토큰을 쿠키에서 확인합니다.
  const token = request.cookies.get('auth-token');

  // 유효한 토큰이 없으면 로그인 페이지로 이동
  if (!token) {
    return NextResponse.redirect(new URL('/login', request.url));
  }
  
  // 토큰이 확인되면 요청 그대로 통과
  return NextResponse.next();
}

// 이 미들웨어가 /admin 이하의 모든 경로에 적용되도록 설정
export const config = {
  matcher: '/admin/:path*',
};
```
2. 지역 & 언어 기반 리디렉션
	방문자의 브라우저 언어나 지역 정보를 바탕으로 알맞은 언어의 페이지로 안내함
	클라이언트 요청의 Accept-Language 헤더를 읽어서
	한국어 사용자가 접속했다면 /ko 페이지로 리디렉트하는 방식이다.
```ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  const acceptLang = request.headers.get('accept-language');
  if (acceptLang && acceptLang.startsWith('ko')) {
    // 한국어를 사용하는 경우 한국어 페이지로 리디렉트
    return NextResponse.redirect(new URL('/ko', request.url));
  }
  return NextResponse.next();
}

// 모든 루트 경로에 대해 적용
export const config = {
  matcher: '/',
};
```
3. A/B테스트 및 기능 플래그
	사용자 그룹에 따라 다른 버전의 페이지를 제공하여, 실험이나 기능 활성화를 수행
	무작위로 사용자를 두 그룹으로 나누거나 쿠키에 저장된 플래그 값을 기준으로
	서로 다른 버전의 콘텐츠를 보여준다.
```ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  // 예: 무작위로 50% 확률로 두 버전을 배포
  const isVariantA = Math.random() < 0.5;
  const variantPath = isVariantA ? '/variantA' : '/variantB';
  return NextResponse.rewrite(new URL(variantPath, request.url));
}

export const config = {
  matcher: '/landing-page',
};

```