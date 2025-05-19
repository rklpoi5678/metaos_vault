---
type: project
theme: project
flow: 실현
insight_level: 3
related_framework:
  - FLOW
  - DIKI
  - PATH
  - DISCOVER
  - LEAN
  - TanaTool
  - POS
meta_layer: true
---
[[Home]]
[[00_STR__DIKI_Structure]]
[[03_STR__PATH_Structure]]
[[95_STR__AI_Tool]]

정보 수집부터 실행까지 자동화하는 지식 성장 프로그램
인터넷 정보 자동화 수집 → 분석 → 실행 시스템 로 이어지는 AutoInsight Flow

---
## 목적

인터넷의 긴 글(뉴스, 논문, 블로그 등)을 자동화로 수집 → 분석 → 정보화 → 실행 가능한 콘텐츠로 재정리하는 시스템 구축

- **기본 전제**: 최대한 무료 툴을 활용
- **중심 툴**: ChatGPT(딥샤크 정도 체급) + NotebookLM + Obsidian
- **보조 툴**: Liner, Copilot, Claude, Felo, Google AI Studio(재미니), Tiro, Krea AI, PDFMathTranslate, DeepL, 울프람알파, Elicit 등

---
## 1단계: 정보 수집 (웹스크래핑 or 수동 업로드 기반)

### 자동화 방식 (가능하면 무료)

- **수동 업로드 (기본)**
    
    - Notion Web Clipper
        
    - Obsidian Web Clipper (경로는 Inbox->Capture로)
        
- **자동 수집 (추가 옵션)**
    
    - RSS 수집기 → Zapier / Make로 Notion 연동
    - Python + BeautifulSoup으로 웹스크래핑
    - PDF → OCR 자동 변환 (PDFMathTranslate등)

---

## 2단계: 구조 파악 / 인사이트 추출

### 분석 툴 & 활용

- **NotebookLM**: 긴 문서 요약, 구조 파악
    #NotebookLM
- **Google AI Studio**: 도표/차트 뽑기, 음성파일 분석
   #GoogleAIStudio 
- **Claude**: 논문 수준 요약, 주제 정리, 보고서 스타일 변환
    #Claude

더 자세한 내용
[[06_STR__NotebookLM_Tool]]

---

## 3단계: 자동 정리 & 연결

### 도구 추천

- **Obsidian**
    #LENS #프레임워크
- **Notion**: 데이터베이스 기반 정리, 프론트 뷰 역할
    #Notion 
- **Tiro**: 회의용 메모, 음성에서 문서 자동화
    #Tiro

- 수집된 정보 → Obsidian 메모화 → Notion에서 실행체계/대시보드 구성
    
+ 추가적으로 분석된 음성을 데이터분석기법을 활용하여 감정점수를 매기거나 단어 카운트가능
+ 분석된 음성을 이용하여 요약 메모화 가능

---

## 4단계: 실행 콘텐츠 제작/학습

### 자동 콘텐츠 제작

- **ChatGPT**: 콘텐츠 구조화, 활용 방안 제안
    #ChatGPT
- **Miricanvas/Krea AI**: 시각화 보조 (썸네일, 다이어그램 등)
- 추가로 재미니 나 구글의 생태계를 이용하는게 좋습니다.
   #미리캔버스 #KreaAI
- **PDFMathTranslate/DeepL**: 번역용
    #PDFMathTranslate


---

## 💡 핵심 원칙

- "데이터는 수집이 아니라 **활용이 목적**이다."

- "**정보를 인사이트로**, **인사이트를 행동으로 전환시켜야 진짜 생산성**이다."

- "자동화는 인간의 창의력을 증폭시키는 방향으로 설계한다."
    

---

## 확장성(업데이트 가능)

- SEO / 마케팅 자동화 도구들과 연동 가능
    
- 수익화 단계에서 콘텐츠 기반 분석 보고서 판매 가능
    
- 사용자가 원하는 콘텐츠 요약·분석 대행 서비스도 가능
    .
    .
    .

---

## ✅ 우선 해야 할 일

1. 정보 수집 체계 구축  [[Flow_manual_Obsidian.md]] ! 또한 Flow_Engine프로젝트 성실히 완수
    
2. NotebookLM / Google AI Studio로 기본 템플릿 확보 & 반복
    
3. Notion에 자동화 흐름을 정리한 대시보드 만들기 (꼭 Notion이 아니어도 됨)
    - 옵시디언은 기본적으로 마크다운 문서를 제공하여 확장성이 뛰어나다는 장점이용

4. 프롬프트 세트 표준화 (업무/학습/요약용)
	- AI용 인공지능 활용(기술이용하기)
