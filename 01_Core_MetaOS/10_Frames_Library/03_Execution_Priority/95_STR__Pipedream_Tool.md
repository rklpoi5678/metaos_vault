> **도구 타입: 실행 자동화 트리거**  
> **용도: 조건 충족 시 외부 동작 호출**

### 💡 예시 시나리오:

- Obsidian에서 `status: ready_to_launch` 로 설정된 노트가 있을 때
    
- 자동으로 Notion DB에 등록 + 슬랙에 메시지 발송
    


Trigger: Obsidian note updated → 조건 검사 
→ Action: Notion API 호출 + Slack 메시지 전송`

👉 DSL 상에서 `TRIGGER → ACTION` 자동 전이 구조에 대응됨  
→ `STATE_CHANGE` 또는 `COMMIT_POINT` 발생 시 실행됨