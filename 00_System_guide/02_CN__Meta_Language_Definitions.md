---
type: Core
theme: Core
flow: meta_structure
insight_level: 4
related_framework: 
meta_layer: true
---

## 온라인 메타 언어 정의

제목: [우선순위_2자리]_[역할약어]__[기능설명].md

00_OV__개요와문서구조.md (Overview) 
01_MX__메타설계프레임정리.md (Meta indeX) 
02_FR__프레임워크정리.md (Framework) 
03_EX__실험및응용사례.md (EXperiment) 
04_FN__기능설계.md (FuNction) 
05_DG__시각화도식.md (DiaGram) 
99_AR__아카이브.md (ARchive) 

파일 시스템: snake_case -> 옵시디언 네임은 00_0V_개요와 흐름 처럼 표시
URL파싱은 kebab-case
내부노드는 kebab-case나 camelCase나 PascalCase 썩어서 사용가능(자유도)

(다만 한 파일의 중요도가 높으면 내부노드라도 파일 시스템 명명을 사용)
( _IN1__ 처럼 우선도가 인거나 높을시 1~N순서로 가능함)

## [약어 표준화] – 역할을 체계화하기 위한 2자리 코드

| 약어  | 의미         | 사용 문맥 예시                |     |     |
| --- | ---------- | ----------------------- | --- | --- |
| OV  | Overview   | `00_OV__전체개요`           |     |     |
| MX  | Meta indeX | `01_MX__메타구조정리`         |     |     |
| FR  | Framework  | `02_FR__FLOW_프레임`       |     |     |
| EX  | Experiment | `03_EX__실전_테스트기록`       |     |     |
| FN  | Function   | `04_FN__루틴설계`           |     |     |
| DG  | Diagram    | `05_DG__구조도시각화`         |     |     |
| AR  | Archive    | `99_AR__보관용`            |     |     |
| CN  | Concept    | `06_CN__설계개념정의`         |     |     |
| ST  | Story      | `07_ST__사용자시나리오`        |     |     |
| PR  | Prompt     | `08_PR__명령어셋`           |     |     |
| IN  | Insight    | `09_IN__실험인사이트`         |     |     |
| TL  | Tool       | `10_TL__도구연동정리`         |     |     |
| _   | connect    | `_Templates_log`        |     |     |
| EG  | Example    | `11_EG__파인만학습기법`        |     |     |
| STR | Structure  | `12_STR_FLOW_Structure` |     |     |
| FB  | Feedback   | `13_FB_Project`         |     |     |

이 표는 **추가 가능**하고, **커스텀도 가능**
중요한 건 **일관성과 구조적 호출 용이성**

### 숫자네이밍 규칙
00 ~ 09: 기능 순서(우선순위로 오름차순정렬)
10 ~ 90: 라이브러리 순서(우선순위로 오름차순정렬)
90 ~ 99: 보조기능
## 내부 노드에서 사용하는 네이밍 방식(camelCase/PascalCase)

## 루틴 설계 흐름
camelCase (실행 루틴, 문맥 연동, 속성 호출)
예시:
- dailyCheckRoutine  
- morningBoostTrigger  
- contentUploadFlow  
- makeTaskList 
- 그래프 뷰에서 깔끔하게 뜨고
- 특히 자동화 툴이나 Obsidian Dataview랑 연동 시 최적

## 연결 구조
PascalCase (노드명, 핵심 키워드, 링크 명)
예시:
- [[FlowOS]]  
- [[EmotionLoop]]  
- [[PLRProject]]  
- [[ExecutionTensionProtocol]]  
- 인덱싱, 검색, 링크 정렬 시 압도적으로 깔끔해짐


## 정리: 외부는 [숫자__약어__설명], 내부는 camelCase / PascalCase


## 오프라인 메타 언어 정의

제목: [우선순위_2자리]_[역할약어]__[기능설명].md (온라인과 동일)

단 ⭐ 03_FR__프레임워크정리 같이 별표는 "중요도높으니 후속 작업이 필요하다라는뜻입니다."
또한 ⭐ 03_FR__프레임워크정리. 나 체크박스 기호를 추가하여 해당 노트가 '처리중,'보류','완료'를 나타낼수있다.

메타데이터를 넣는다
(날짜|TMP|제목)
TMP: 임시 아이디어
ND: 검토 필요
폐기예정: 전체 체크나 DEL의 심볼

기본 기호
제목 앞 
"• "표시시는 (Task)
해야 할 작업 또는 할일
">" 표시는 이월한다라는 의미
"<" 표시는 재조정된 작업

"○ "표시는 (Event)
회의, 약속, 데드라인 등 일정 관련 항목

"–" 표시는 (Note)
정보,아이디어,참고 사항 등 작업이나 일정 외의 내용을 기록 할떄 사용

"!","별"은 (Priority)
특히 중요한 작업이나 우선순위가 높은 항목을 강조할때
"?" (Review Needed)
추가 정보나 의문이 있는 항목을 표시


"()"는 추가설명or정보를 표시할때
"[]"는 리스트처럼 무언가를 여러개 담을때, 태그, 메타정보
"" 는 인용,핵심,특정용어 강조시
"/"는 대치 관계 or 복수 항목 or 시간 날짜
"|"는 복수의 정보를 한줄에 배열시 구분자로 ,메타정보 연결 구분자
"{}" 딕셔너리처럼 그룹화 / 메타정보 그룹화

"~"는 내가 생각해서 더 작성하거나 / 흐름 / 까지라는 뜻
---[내일 작성]---: 선3개와 3개로 닫고 []이 가운데는 조건을 나타냄

### ! 이런 속성이나 제목 구조를 영어로 하는이유
유용성, 확장성, 언어문제(언어구조 문제등) 어느정도