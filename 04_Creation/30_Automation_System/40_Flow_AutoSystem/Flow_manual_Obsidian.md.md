---
type: insight
theme: 자동화
flow: 자동화
insight_level: 2
related_framework: [FLOW]
meta_layer: true
---


## 📥 정보 수집 체계 구축 (Obsidian용)
[[Home]]
[[00_OV__Autolnsight_Flow]]
[[실행 플로우.md]]

---

### ✅ 목적

- 인터넷 상의 글, 논문, 뉴스, 블로그 등을 빠르게 수집하고, 정리된 형태로 분석 가능하도록 만드는 체계 구축
    
- Obsidian과 Notion을 중심으로 데이터베이스화 및 후속 분석 흐름 연결
    

---

### 🧱 수집 단계 구조 (3 Layer)

#### 1. 수동 수집 (기본) [[LENS 정보 수집 체계 수동 보완 계획 (불편함).md]]

- **도구**: Notion Web Clipper, Glasp, Liner, 라이너
    
- **대상**: 블로그 글, 뉴스기사, 논문 링크, SNS 콘텐츠
    
- **방법**:
    
    - 크롬 확장기능을 활용하여 직접 클리핑
        
    - 하이라이트 → 메모 → Notion에 자동 저장
        

#### 2. 반자동 수집 (연결 자동화)

- **도구**: RSS Feed + Notion API or Zapier
    
- **대상**: 즐겨찾는 블로그, 뉴스 RSS
    
- **방법**:
    
    - RSS 피드 구독 → Zapier로 Notion에 자동 저장
        
    - 특정 키워드 포함 여부로 필터링 가능
        

#### 3. 자동 수집 (개발 연동)

- **도구**: Python (BeautifulSoup / Selenium), Google Sheets API
    
- **대상**: 반복되는 구조의 웹사이트
    
- **방법**:
    
    - 크롤링 코드 작성 (구조화된 HTML 대상)
        
    - 정기적으로 실행 후 Google Sheets로 데이터 정리
        
    - Notion / Obsidian으로 가져오기
        

---

### ⚙️ 실행 방법 순서도

```
1. 정보 수집 목적 정의 (ex. 마케팅, 논문 요약, 트렌드 분석)
2. 수집 대상 선정 (뉴스, 논문, 블로그 등)
3. 수동 수집 도구 설치 및 연동 (Notion Web Clipper, Glasp 등)
4. Notion에 카테고리별 페이지 or DB 생성
5. 수동 수집 테스트 및 구조 정의 (태그 / 메모 구조)
6. Zapier or Make를 활용한 반자동 RSS → Notion 자동화
7. 고정 수집처가 있을 경우 Python으로 자동 수집 코드 작성
8. 정기 수집 및 Obsidian 동기화 설정
```

---

### 📁 Obsidian 구조 예시

```
📁Inbox/수집자료
  └─ 2025-04-08_뉴스_마케팅트렌드.md
  └─ 2025-04-08_블로그_SEO전략.md

📁Reference/데이터
  └─ 키워드 요약.md
  └─ 도구별 정리.md

📁Projects/자동화시스템
  └─ AutoInsight 개요.md
  └─ 정보수집 체계 구축.md
```

---

### 🔁 연결 방법

- 수집된 문서는 정리 후 Obsidian L.E.N.S 프레임워크 기반으로 태깅 및 링크
    
- 정리된 정보는 분석툴 (NotebookLM, Claude 등)으로 넘어가 인사이트 추출
    
- 정기적으로 수집 → 구조화 → 분석 → 콘텐츠화 루틴 수행