
## 핵심
프론트엔드 테스트 (Canvas UI, 사용자 인터렉션이 핵심이다.)
- 단위 테스트 (Unit Test): 개발 컴포넌트나 함수가 예상대로 동작하는지 확인하는것이다.
- 도구: React(Jest(Vitest) + React Testing Libray) - Vue(Jest(Vitest) + Vue Test Utils) + Angular(Jasmine + Karma)

- 통합 테스트(Integration Test): 여러 컴포넌트나 모듈이 함께 작동할 때의 상호작용 확인
- 단위 테스트 도구를 확장하여 사용 (React Testing Libray등으로 충분히 가능)

- 종단 간 테스트(End-to-End, E2E Test): 실제 사용자의 흐름(로그인, 도형 추가, 편집, 저장 등)을 시뮬레이션하여 전체 시스템이 작동하는지 확인, 뚝딱이 서비스에 특히 중요하다.
- 도구: Cypres(작관적이고 강력하며, 디버깅이 용이, 웹 앱에 최적화),
- Playwright: (Chromium, Firefox, WebKit등 다양한 브라우저 지원, 병렬 실행 강력)
- Selenium: (가장 오래되고 광범위하게 사용되지만 설정이 복잡할수 있다.)

백엔드 테스트 (API,DB 연동)
- API 엔드포인트, 비즈니스 로직, 데이터베이스 연동 등이 올바르게 작동하는지 확인
- 도구: Jest, Mocah + chai, supertest(API테스트)
- Python: Pytest, unittest

## CI/CD 파이프라인 연동 (GitHub Actions)
- 대부분의 CI/CD툴은 YAML 파일을 통해 파이프라인을 설정, GitHub저장소를 이용한다면. GitHub Actions가 연동하기 매우 편리하다.

```bash

name: CI/CD Pipeline for Ttuktaki Service

on:
  push:
    branches:
      - main # main 브랜치에 코드가 푸시될 때마다 실행
  pull_request:
    branches:
      - main # main 브랜치로 PR이 생성/업데이트될 때마다 실행

jobs:
  build_and_test:
    runs-on: ubuntu-latest # 파이프라인이 실행될 가상 환경

    steps:
    - name: Checkout code
      uses: actions/checkout@v3 # 저장소 코드 가져오기

    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18' # Node.js 버전 설정

    - name: Install Frontend Dependencies
      run: |
        cd frontend # 프론트엔드 폴더로 이동
        npm install

    - name: Run Frontend Unit Tests
      run: |
        cd frontend
        npm test # Jest (혹은 다른 단위 테스트) 실행

    - name: Install Backend Dependencies
      run: |
        cd backend # 백엔드 폴더로 이동
        npm install

    - name: Run Backend Tests
      run: |
        cd backend
        npm test # Jest/Pytest 등 백엔드 테스트 실행

    # E2E 테스트 (Cypress 예시)
    - name: Start Frontend Server for E2E
      run: |
        cd frontend
        npm start & # 백그라운드에서 프론트엔드 서버 실행
      env:
        CI: true # CI 환경임을 명시 (일부 개발 서버는 CI=true일 때 Headless 모드로 실행되기도 함)

    - name: Start Backend Server for E2E
      run: |
        cd backend
        npm start & # 백그라운드에서 백엔드 서버 실행

    - name: Wait for Servers to be Ready
      run: sleep 10 # 서버가 완전히 구동될 때까지 잠시 대기 (필요시 더 정교한 방법 사용)

    - name: Run Cypress E2E Tests
      run: |
        cd frontend # Cypress가 설치된 곳으로 이동
        npm run cypress:run # Cypress 테스트 실행 (Headless 모드)

    # 시각적 회귀 테스트 (선택 사항, Cypress-image-snapshot 사용 예시)
    # - name: Run Visual Regression Tests
    #   run: |
    #     cd frontend
    #     npm run cypress:run -- --env CI=true --config fixturesFolder=cypress/snapshots/fixtures --spec cypress/e2e/visual.cy.js # 특정 시각적 테스트 스펙 실행
    #   env:
    #     CI: true
    #     # CYPRESS_SNAPSHOT_UPDATE: 'true' # 스냅샷 업데이트 시 수동으로 활성화 (로컬에서만 권장)

    # 배포 단계 (선택 사항, 테스트 통과 시에만 실행)
    # - name: Deploy to Staging
    #   if: success() && github.ref == 'refs/heads/main' # 모든 테스트 통과 & main 브랜치 푸시 시에만 배포
    #   run: |
    #     # 여기에 배포 스크립트 작성 (예: AWS [[[[S3]]]], Vercel, Netlify, Docker Hub 등)
    #     echo "Deploying to staging environment..."
    #     # 예: aws [[s3]] sync ./build [[s3]]://your-staging-bucket --delete
```

