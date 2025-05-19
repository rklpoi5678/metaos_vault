# metaOS 개요 및 MVP 구현 계획

## 기본 철학
metaOS는 **정적 노트 템플릿**이 아닌, **“실행 흐름을 생성하고 조율하는 시스템”**으로 설계되어야 합니다.

## 작동 구조
1. **입력**: 나의 상태, 감정, 아이디어
2. **분석**: metaOS 철학 기반 구조 매핑
3. **출력**: 루틴/노트 생성, 실행 안내
4. **기록**: 감정 로그, 루틴 이력
5. **반복**: 루프 + 진화

## 기능 구성 예시

| 기능 모듈         | 설명                                     |
| ------------- | -------------------------------------- |
| **의도 입력기**    | 감정 및 상태 입력 (텍스트/선택지)       |
| **구조 매핑 엔진**  | 입력값을 DIKI / FLOW / POS 등으로 해석  |
| **루틴 제안기**    | 현재 상태에 맞는 실행 루틴 자동 생성    |
| **노트 자동 생성기** | 선택한 흐름으로 노트/루틴 문서 자동 출력 |
| **감정 리듬 기록기** | 감정 및 실행 상태 시각화               |
| **템플릿/루틴 공유** | 흐름을 커뮤니티에 공유/클론 가능       |
| **자기 OS 저장소** | metaOS 구조 저장 및 불러오기, 복제 가능 |

## 기술 스택 추천 (최소 MVP 기준)

| 파트             | 스택                                      |
| -------------- | --------------------------------------- |
| **Frontend**   | Next.js + TailwindCSS + Zustand         |
| **Backend**    | Node.js(Express) or Supabase            |
| **DB**         | PostgreSQL                               |
| **AI 연동 (선택)** | OpenAI API로 입력 분석 및 루틴 제안   |
| **배포**         | Vercel + PlanetScale or Supabase        |

## 기본 화면 구성 예시

- **Home**: 오늘 상태 입력
- **OS Studio**: metaOS 구조 편집기
- **Routine Hub**: 추천 루틴/실행 흐름 선택
- **Logbook**: 감정/실행 이력 시각화
- **ShareSpace**: 다른 사람의 metaOS 흐름 구경 & 가져오기

## 실행 시나리오 예시

**User**: “오늘은 멍하고 뭔가 안 되고 막힌다…”

**metaOS 반응**:
- 감정: 흐림 / 무기력
- 실행 권장 구조: FLOW + 감정 회복 루틴
- 루틴 제안: 3문장 감정 드로잉 + 파열 루틴 1개 실행
- 노트 생성 완료: “2025-04-18_감정재기루틴.md”
- 실행 리듬 추적: 리듬맵에 기록됨

## 결론: metaOS 웹 기반화의 필요성

- 개인의 리듬, 실행, 철학을 다른 사람도 활용할 수 있도록 해야 합니다.
- metaOS는 웹 기반에서 “흐름이 돌아가야” 진정한 OS가 됩니다.

## 즉시 실행 시작 포인트 제안 (순서)

1. **metaOS 구조를 JSON/YAML로 정의 (모듈화)**
2. **Next.js MVP UI 구성 (루틴 생성기, 감정 입력기, 기록 뷰어)**
3. **노트 자동 생성 로직 연동 (Markdown 파일 다운로드 or 서버 저장)**
4. **버전 0.1: 자기 metaOS 구성 + 루틴 실행 + 감정 기록 완성**

## Q1: MVP에서 “살아있음”을 느끼게 할 기능

**답변**: “지금 내 감정이나 상태를 입력하면, 바로 실행 루틴이 생성되어 나를 움직이게 해주는 것.”  
이 기능 하나만 구현되면 metaOS는 **“살아있는 것”**으로 인식될 수 있습니다.

## 왜 이 기능이 ‘살아있음’을 느끼게 하냐?

1. **즉각적 반응**: 입력에 대한 해석과 실행 제공
2. **루틴화**: 감정, 철학, 실천이 반영된 구조
3. **구조적 안내**: 개인 맞춤형 흐름 제공

## 구현 예시 MVP 흐름 (ver. 0.1)

1. **사용자가 감정/상황 입력**: “지금 뭔가 무기력하고, 아무 생각도 안 나.”
2. **metaOS 반응**:
   - 감정 진단: 무기력 + 정체
   - 구조 진단: FLOW 루틴 단절 / DIKI 인풋 고갈
   - 실행 루틴 추천:
     - [ ] 3문장 자유 연상 글쓰기
     - [ ] 시각자극 루틴: 좋아하는 이미지 10장 리서치
     - [ ] 무작위 키워드로 말 만들기 (Random Word Loop)
3. **3초 안에 실행**: “3문장 연상 글쓰기 시작”

### 결과
- 실행 루틴 자동 생성
- 노트 자동 생성 (`/240418_감정루틴.md`)
- 실행 후 감정 기록
- 사용자: **"내 상태에 맞게 누가 나를 구조화해주는 느낌"** → **살아있다고 느낌**

## 다음 행동
- 감정/상황 입력 → 구조 분석 → 루틴 출력 → 즉시 실행  
이 4단계만 되는 구조를 **웹 MVP로 만들면**, metaOS는 ‘살아 있다’는 느낌을 첫 사용부터 심어줄 수 있습니다.


### `users`

| 필드명        | 타입       | 설명          |
| ---------- | -------- | ----------- |
| id         | UUID     | 고유 사용자 ID   |
| email      | string   | 사용자 이메일     |
| name       | string   | 닉네임/표시명     |
| created_at | datetime | 가입일         |
| settings   | JSON     | 사용자별 커스터마이징 |

---

### `projects`

| 필드명        | 타입       | 설명            |
| ---------- | -------- | ------------- |
| id         | UUID     | 프로젝트 ID       |
| user_id    | UUID     | 사용자 ID (외래키)  |
| title      | string   | 프로젝트명         |
| status     | enum     | 진행중 / 완료 / 중단 |
| template   | string   | 사용한 템플릿 이름    |
| created_at | datetime | 생성일           |
| tags       | array    | 사용자 태그        |

---

### `project_nodes` (폴더/파일 구조 저장용)

| 필드명        | 타입        | 설명                      |
| ---------- | --------- | ----------------------- |
| id         | UUID      | 노드 ID                   |
| project_id | UUID      | 소속 프로젝트                 |
| type       | enum      | 'folder' / 'file'       |
| title      | string    | 노드명 (00_개요 등)           |
| content    | text/JSON | 마크다운 or 노트 본문           |
| order      | int       | 정렬 순서                   |
| parent_id  | UUID      | 폴더 구조 트리용 (null = root) |

---

### `routines` (Flow Tracker 전용)

| 필드명          | 타입         | 설명                      |
| ------------ | ---------- | ----------------------- |
| id           | UUID       | 루틴 ID                   |
| project_id   | UUID       | 소속 프로젝트                 |
| title        | string     | 루틴명                     |
| frequency    | string     | daily / weekly / custom |
| trigger      | string     | 감정 기반 트리거 (선택)          |
| completed_at | datetime[] | 체크 기록                   |
| active       | boolean    | 현재 실행 중 여부              |

---

### `outputs`

| 필드명        | 타입       | 설명                    |
| ---------- | -------- | --------------------- |
| id         | UUID     | 출력물 ID                |
| project_id | UUID     | 연결된 프로젝트              |
| format     | enum     | pdf / notion / json 등 |
| published  | boolean  | 마켓 등록 여부              |
| url        | string   | 배포 링크                 |
| created_at | datetime | 생성일                   |

### 1️⃣ Supabase 프로젝트 생성

1. Supabase에 가입하고 로그인합니다.
    
2. **New Project**를 클릭하여 새 프로젝트를 생성합니다.
    
3. 프로젝트 이름, 데이터베이스 비밀번호, 지역을 설정하고 **Create new project**를 클릭합니다.
    

### 2️⃣ 테이블 생성

1. **Table Editor**로 이동합니다.
    
2. **Create new table**을 클릭하여 각 테이블을 생성합니다.
    
3. 각 테이블의 필드를 정의하고 데이터 타입을 설정합니다.
    
    - `users`, `projects`, `project_nodes`, `routines`, `outputs` 테이블을 각각 생성합니다.
        
    - `id` 필드는 **UUID**로 설정하고, `created_at` 필드는 **timestamp**로 설정합니다.
        
    - `user_id`, `project_id` 등은 **외래키(Foreign Key)**로 설정하여 관계를 맺습니다.
        

### 3️⃣ 테이블 간 관계 설정

1. **Foreign Key**를 설정하여 `projects.user_id`가 `users.id`를 참조하도록 합니다.
    
2. `project_nodes.project_id`가 `projects.id`를 참조하도록 설정합니다.
    
3. `routines.project_id`가 `projects.id`를 참조하도록 설정합니다.
    
4. `outputs.project_id`가 `projects.id`를 참조하도록 설정합니다.
    

### 4️⃣ 데이터 접근 권한 설정 (RLS)

1. **Row Level Security (RLS)**를 활성화하여 사용자별 데이터 접근을 제한합니다.
    
2. `users` 테이블은 각 사용자가 자신의 데이터만 조회할 수 있도록 정책을 설정합니다.
    
3. `projects` 테이블도 해당 사용자의 프로젝트만 조회할 수 있도록 설정합니다.
    

### 5️⃣ API 및 인증 설정

1. Supabase는 자동으로 RESTful API를 제공합니다.
    
2. **Auth 설정**을 통해 이메일 로그인, OAuth 등을 활성화할 수 있습니다.
    
3. `users` 테이블과 연결하여 사용자 인증을 구현합니다.
    

### 6️⃣ 데이터 삽입 및 테스트

1. **Insert row**를 클릭하여 샘플 데이터를 추가합니다.
    
2. `users` 테이블에 테스트 계정을 생성하고, `projects` 테이블에 샘플 프로젝트를 추가합니다.
    
3. API를 호출하여 데이터가 정상적으로 저장되고 조회되는지 확인합니다.
    

### 7️⃣ 클라이언트 연동

1. **Supabase SDK**를 설치합니다:
    
    bash
    
    ```
    npm install @supabase/supabase-js
    ```
    
2. 클라이언트에서 Supabase를 초기화합니다:
    
    js
    
    ```
    import { createClient } from '@supabase/supabase-js';
    
    const supabaseUrl = 'https://your-project.supabase.co';
    const supabaseKey = 'your-anon-key';
    const supabase = createClient(supabaseUrl, supabaseKey);
    ```
    
3. 데이터를 가져오는 API를 구현합니다:
    
    js
    
    ```
    const { data, error } = await supabase
      .from('projects')
      .select('*')
      .eq('user_id', 'your-user-id');
    ```
    

### 8️⃣ 배포 및 운영

1. Supabase 프로젝트를 **Production 모드**로 설정합니다.
    
2. **백업 및 모니터링**을 설정하여 데이터 안정성을 확보합니다.
    
3. **웹 애플리케이션과 연동**하여 실제 서비스로 운영합니다.
    

이제 Supabase를 활용하여 프로젝트를 구축할 준비가 완료되었습니다! 🚀 추가적인 설정이 필요하면 Supabase 공식 문서를 참고하세요. 어떤 부분이 가장 궁금한가요? 😊

## 중앙공간

| MicroSaaS 유형 | 중앙 공간 구성                 |
| ------------ | ------------------------ |
| 콘텐츠 생성기      | 프롬프트 입력 + 결과 카드 뷰        |
| 분석 도구        | 데이터 입력 + 시각화 차트          |
| PDF 처리       | PDF 업로드 + 자동 요약/태그 출력    |
| 일정/루틴        | 일정 입력 + 타임라인 UI          |
| GPT 프롬프트 도구  | 입력 + 토큰/상태 시각화 + 저장 영역   |
| 개인화된 AI 도우미  | 상태 입력 + 실시간 응답 + 리마인더 카드 |
| MetaOS 구조    | 중앙 역할                    |
| Core         | 지금 유저의 목표/질문이 표현되는 공간    |
| Structure    | 기능 흐름을 직관적으로 연결          |
| Tool         | 클릭/입력/조정 가능한 상호작용 컴포넌트   |
| Experiment   | 실험/피드백/루틴 자동 저장          |
| Archive      | 작업물 저장, 다운로드, 결과 복기 가능   |
[프로젝트 진입]
→ Core 불러오기
→ Structure 선택 (기능 설계 / 루틴 선택 등)
→ Tool 조작 (입력/토글/설정)
→ 실험 실행 / 프리뷰
→ Archive에 저장 (또는 계속 실험)

```json
{
  "project_id": "string",
  "core_statement": "string",
  "structures": [
    {
      "type": "experiment" | "feature_design" | "routine",
      "title": "string",
      "tools_used": ["GPT", "Timeline", "Prompt_X"],
      "inputs": { "key": "value" },
      "outputs": { "type": "chart" | "text" | "component", "content": "..." },
      "archive_note": "string",
      "created_at": "timestamp"
    }
  ]
}
```

## 오른쪽 구간

💡 작동 흐름 예시
사용자가 실험 중 →
오른쪽 패널에:

현재 Structure 흐름 간단 요약

사용 중인 Tool 리스트

실험 목적이 Core와 맞는지 체크

“지금 실험, 이전 루틴과 비슷합니다. 불러올까요?”

“이 상태에선 감정 루틴 루프가 유효합니다” → 바로 연결

➡ 중앙은 몰입,
➡ 오른쪽은 메타-정렬 + 제안 + 트리거 발생기


## 🧠 결과적으로

> 오른쪽 보조패널은 **MetaOS의 리듬 제어 시스템이다.**  
> 사용자 감정, 실험 상태, 구조 흐름을 감지하고  
> **“다음 어디로 갈지”를 제안하는 존재 기반의 GPT 보조 브레인**

---

## ✨ 정리 선언

> **“오른쪽 보조패널은 정보창이 아니라,  
> 현재 상태를 감지하고 리듬을 조절하며  
> 실험 루프와 구조 간 흐름을 이어주는 존재형 메타 인터페이스다.”**