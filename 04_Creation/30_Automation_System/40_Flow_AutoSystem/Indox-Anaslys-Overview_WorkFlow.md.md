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
[[06_STR__NotebookLM_Tool]]
[[Flow_HalfSystem_Overview.md]]
[[실행 플로우.md]]
[[Flow_manual_Obsidian.md]]


## 🎯 목적
- 정보 출처 신뢰성과 정확도에 따라 흐름을 다르게 설계
- 자동화는 목적이 명확할 때만 도입

---

## 📌 주요 분기

### 1. 분석 정확도 필요한 흐름 (기업 분석, 시장 조사 등)
- ChatGPT로 검색 흐름도 및 방법론 설계
- Liner / Copilot / Gemini→ 수동 클리핑
- Obsidian에 저장 후 PDF로 변환
- NotebookLM으로 요약/인사이트 추출

### 2. 가벼운 정보 (뉴스, 취미, 지식 등)
- Python/스크래핑 툴로 자동 수집
- 한데 모은 후 PDF화
- NotebookLM 분석 → 보류(추후 자동화 가능성)

---

## 🛠️ Make의 사용 원칙

- SaaS나 앱 내 반복적인 작업 자동화
- 불필요한 루틴은 과감히 생략
- 자동화는 도구의 목적이 뚜렷할 때만 채택

---

## 🗂 추천 정리 방식

- `/Inbox/수집` → 원본 정보
- `/Projects/조사명` → PDF + 요약 정리
- `/Insights` → 정제된 인사이트 통합

**“NotebookLM은 요약기계가 아니라, 흐름 분석 도우미”**라고 생각해.

프롬프트에서 “정리”만 요구하면 피상적인 결과가 나올 수 있다.
**실제 실행을 위한 흐름**이나 **자기화 전략**을 요구하면  진짜 제대로 된 답을 끌어낼 수 있다.