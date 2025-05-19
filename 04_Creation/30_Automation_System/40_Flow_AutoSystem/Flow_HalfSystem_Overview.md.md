---
type: insight
theme: 자동화
flow: 자동화
insight_level: 2
related_framework: [FLOW]
meta_layer: true
---


[[Home]]
[[00_OV__Autolnsight_Flow]]
[[Flow_manual_Obsidian.md]]

현재 RSS가 더효율적이라 판단
graph TD
A[RSS 주소 수집] --> B[Zapier or Make로 자동화 연결]
B --> C[Notion DB 저장 (정보수집_RAW)]
C --> D[Obsidian으로 마크다운 동기화]
D --> E[인사이트 추출, LENS 연결]

rss주소확보
notiondb구성 이전(정보수집_RAW)
Zapier/Make 연결
둘중하나

#### Zapier

- Trigger: RSS → 새 글 등록
    
- Action: Notion → 새로운 row 생성
    
- 요약 자동 생성은 ChatGPT API로 붙일 수도 있음 (원한다면 구조 공유 가능)
    

#### Make (인테그로마트)

- RSS 모듈 → Notion 모듈 → Markdown으로 export 가능
    
- 유연하게 태그 분기, 글자 수 조건 등도 설정 가능
### 🔁 전체 흐름 개요

**웹에서 읽기 → Glasp 하이라이트 → Notion 자동 기록 → Obsidian으로 주기적 통합**

---

## 🧠 [1단계] 정보 수집 & 하이라이트: Glasp 사용

### ⬛ Glasp 설치

- 크롬 확장 프로그램 [Glasp](https://glasp.co/) 설치
    
- Glasp 계정 생성 (Gmail 로그인 추천)
    

### ⬛ 사용 방법

- 웹사이트에서 **텍스트 하이라이트**
    
- 우측 사이드바에 자동 저장됨 (텍스트 + 출처 + 날짜)
    
- **노트/메모**를 추가해도 기록됨 → 이게 나중에 Obsidian 메모로 들어감
    

---

## 🔄 [2단계] Glasp → Notion 연동

### ✅ 방법 A: Glasp 자동 연동 기능 (Pro 계정 필요, 테스트 가능)

- Glasp 설정 > `Sync to Notion` 메뉴에서 DB 선택
    
- 연동 시 자동으로 하이라이트가 Notion으로 들어감  
    → 이때 "날짜 / 제목 / URL / 요약 / 메모" 구조로 저장됨
    

### ✅ 방법 B: Zapier or Make 사용 (무료 or 테스트 플랜으로 충분)

- 트리거: Glasp 하이라이트 새로 추가됨
    
- 액션: Notion DB (`정보수집_RAW`)에 자동으로 새 행 추가
    
- 속성 매핑:
    
    - 제목 → 하이라이트한 문장 or 글 제목
        
    - URL → 원문 주소
        
    - 날짜 → 자동
        
    - 요약 or 코멘트 → 메모
        
    - 태그는 수동 입력 or 기본값 설정
        

✅ 템플릿 자동 생성해주는 형태도 가능 (Zapier 템플릿 제공됨)

---

## 🔃 [3단계] Notion → Obsidian 반자동 마이그레이션

### ✅ 방법 A: Notion2Markdown + Dropbox 연동

1. Notion DB를 **마크다운으로 자동 백업**
    
2. Dropbox에 저장
    
3. Obsidian이 Dropbox 폴더를 실시간 감지해서 파일 자동 동기화
    

> 📦 추천 도구:

- [Notion2MD](https://github.com/splitbee/notion2md): CLI 도구 (자동화에 최적)
    
- 또는 [Notion Sync](https://github.com/darobin/notion-sync)
    

### ✅ 방법 B: 매주 Notion에서 "내보내기 → MD파일" 수동 다운로드 후 Obsidian에 붙여넣기

(반자동에서는 이 단계까지만 수동)

---

## ⏳ [4단계] Obsidian에서 정리 및 L.E.N.S 연결

- `/정보수집_RAW` 폴더에 새 파일 저장됨
    
- Weekly Review 노트에서 해당 마크다운 연결
    
- LENS 기준으로 태그 정리 & 인사이트 정리
    

---

## ⛓ 전체 흐름 순서도 요약

mermaid

`graph LR A[웹 아티클 읽기] --> B[Glasp 하이라이트] B --> C[Glasp → Notion 연동 (Zapier or Glasp 자체)] C --> D[Notion2MD 변환] D --> E[Obsidian RAW 폴더로 동기화] E --> F[LENS 연결 및 콘텐츠 확장]`

---

## 🚀 실제로 필요한 도구 리스트

|기능|도구|
|---|---|
|하이라이트 수집|Glasp|
|자동화 연동|Zapier / Make (또는 Glasp Pro)|
|DB 저장|Notion|
|MD 파일 변환|Notion2MD|
|마크다운 지식 관리|Obsidian|
|백업/동기화 (선택)|Dropbox / Git|

---

## ✨ 다음 액션 제안

1. Glasp + Notion 연동 테스트 (Zapier 템플릿 써보기)
    
2. `정보수집_RAW` DB 포맷 Notion에 구성 완료
    
3. Notion2MD 연동 여부 테스트
    
4. Obsidian 폴더 구조에 맞춰 동기화 루트 설계

## 반자동 정보 수집 설계 (RSS 기반 Notion 자동화 흐름)

### 1. 수집 대상 지정

- **타깃 사이트**: 뉴스, 블로그, 논문 아카이브 등
    
- **조건**: RSS 피드가 존재하거나, RSS 생성 가능(Feed43, RSS.app 등)
    

### 2. 도구 준비

- **RSS Reader**: Feedly or RSSHub (수동 확인용 백업)
    
- **자동화 연결**: Zapier 또는 Make 활용
    
- **데이터 저장소**: Notion DB (데이터 구조는 아래 참고)
    

---

## 📊 Notion DB 구조 (RAW 데이터베이스)

|제목|링크|출처|수집일|요약|태그|상태|
|---|---|---|---|---|---|---|
|`[텍스트]`|`[URL]`|`뉴욕타임즈`|`2025-04-08`|`[비워둠 또는 요약봇 연결]`|`#AI`|`수집완료`|

---

## 🔁 자동화 흐름 설계 (Zapier 예시)

1. **Trigger**: RSS Feed에 새 포스트가 올라오면
    
2. **Action 1**: Notion의 특정 DB에 새 Row 생성
    
3. **Action 2 (선택)**: 특정 키워드가 포함되었을 경우 메일/슬랙 알림 발송
    
4. **Action 3 (선택)**: Claude/ChatGPT API를 이용한 요약 삽입 (유료 API 고려 대상)
    

---

## 🎯 단계별 목표 정리

|단계|설명|
|---|---|
|1단계|RSS 타깃 10개 이상 선별 및 정리|
|2단계|Notion DB 및 자동화 연결 (Zapier or Make)|
|3단계|수집된 내용 정리 및 요약 (Claude / NotebookLM 등 연계)|
|4단계|Obsidian으로 주제별 정리 동기화 (분석/학습/인사이트화)|

---

### 참고 도구:

- [Feed43](https://feed43.com): RSS가 없는 사이트에 RSS 생성
    
- [RSS.app](https://rss.app): 비정형 콘텐츠에서 RSS 자동 생성
    
- Notion API: 직접 연결도 

## 🥊 Zapier vs Make 비교표 (2025 기준)
#zapier #make

|항목|**Zapier**|**Make (구 Integromat)**|
|---|---|---|
|**자동화 방식**|직관적 트리거 → 액션 흐름 (선형)|비주얼 플로우, 조건/분기 등 복잡한 워크플로 지원|
|**사용 난이도**|쉬움 (입문자용)|중~고급자 (조금 복잡)|
|**무료 플랜**|월 100개 작업 제한, 5개 Zaps|월 1,000개 작업 가능, 실행시간 15분 제한|
|**유료 플랜 시작가**|$19.99/월|$9/월|
|**RSS 지원**|있음 (단순)|있음 (강력, XPath 필터링도 가능)|
|**Notion 연동**|공식 지원, 매우 안정적|공식 지원, 다만 초반 셋업 복잡|
|**조건 분기 (IF/AND/OR)**|유료에서만 본격 가능|무료에서도 흐름 분기 가능|
|**속도/실행주기**|무료는 15분~30분 간격|무료도 15분 간격부터 가능|
|**커뮤니티/레퍼런스**|많음|많음 (특히 자동화 고수들 선호)|

---

## 🎯 선택 기준 제안

|너의 상황|추천|
|---|---|
|자동화 구조 단순 + 입문자 + 빠르게 테스트하고 싶음|**Zapier**|
|워크플로 분기 + 키워드 필터 + 무료로 다양한 자동화 해보고 싶음|**Make**|
|장기적으로 Notion DB 연동 + 중급 이상 기능 필요|**Make**|
|앞으로도 다양한 API 자동화 활용할 계획 있음|**Make (확장성 매우 좋음)**|
make를 우선체택함
#make

레퍼런스
옵시디언 + NotobookLM PDF통합 고려 (토큰수한정이라는 단점해소가능)
요약/카테고리/태그는 옵시디언 내 플러그인이나 간단한 make플로우에서 정리 가능
이 항목은 
#보류