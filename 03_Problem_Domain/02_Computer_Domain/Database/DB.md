

## Supabase

### Direct Connection
장기 연결용, 데이터베이스에 직접 연결한다.
바로 문 앞까지 직접 가져다 주는 방식

ogr2ogr 명령어로 Supabase에 데이터를 업로드하는 경우 로컬 환경이나 장기적인 연결을 설정하는 작업애 가장 좋다.
### Transaction Pooler
주로 서버리스 함수와 같이 짧고 반복적인 연결이 많은 환경에 유리
미리 풀링하여 처리하기 때문에 빠른 응답이 필요할때 유리하지만 특정 PostgreSQL기능이 제한될수있다.

일회성 주문량이 많거나 급하게 여러 주문을 처리할 때 보통 일회성 주문 이나 서버리스 환경에서쓰임
### Session Pooler
IPv4네트워크 전용으로 권장되는 옵션, Direct Connection의 대안으로 사용 (일반적으로 Direct Connection이 더적합)

Transaction Pooler 처럼 일회성 주문 이나 서버리스 환경

인사이트: supabase랑 postgresSQL은 한패다. 이놈들이 관리하는것은 조심해야된다.
“코드 문제인가?”  
“데이터가 안 들어왔나?”  
“쿼리 실패인가?”

 **“아, PostgreSQL의 RLS 정책이 Supabase 내부에서 기본 차단으로 작동하고 있었구나.”** 

| 상황          | 겉보기 현상                  | 진짜 원인                         |
| ----------- | ----------------------- | ----------------------------- |
| select가 실패함 | `data === null`         | 🔒 RLS 정책 없음                  |
| insert가 안 됨 | 아무 반응 없음                | 🔒 RLS insert 권한 없음           |
| update가 안 됨 | `.update()` 에러          | 🔒 auth.uid() != id           |
| 자동 연동이 안 됨  | 트리거 안 먹음                | 🧨 auth schema는 GUI read-only |
| upsert 실패   | `onConflict`인데 아무 변화 없음 | PK나 index 없거나 틀림              |

기억(Memory): 과거 대화/상태를 저장하고 재사용
학습(learning): 새로운 입력을 받아들여 자기 규칙

## 최대 records수
PostgreSQL 자체는 행의 수에 제한을 두지 않으며, 테이블 크기(예시 32TB)내에서는 원하는 만큼 많은 레코드를 추가할 수 있다.
실제 제한은 사용 가능한 저장 공간과 Supabase프로젝트의 용량 제한에 의해 결정된다.