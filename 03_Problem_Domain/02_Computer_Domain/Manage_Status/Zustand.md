## 상태관리
zustand는 **가볍고 직관적으로 전역 상태를 관리**
특히 로그인 같은 유저 정보, 테마나 감정 모드 같은 설정을 **컴포넌트 트리 밖에서도 깔끔하게 주고받을 수 있는** 게 큰 장점

---

### zustand로 더 할 수 있는 것들

1. **미들웨어 활용**
    - `persist`로 로컬 스토리지에 상태 저장 → 새로고침해도 로그인 유지
    - `redux-devtools`로 상태 변화를 시각화하며 디버깅

2. **모듈화된 스토어 분리**
    
    - `useUserStore`, `useProjectStore`, `useRoutineStore` 등 기능별로 나누면  
        → 코드 가독성↑, 재사용성↑

3. **비동기 처리 간소화**
    
    - `zustand` 내장 `subscribe`나 `zustand/middleware`의 `immer` 등으로  
        → API 호출 → 상태 갱신 흐름이 한곳에서 관리돼

4. **경량성 유지**
    
    - 불필요한 리렌더링 제어 가능 (selector 활용)
    - Context + useReducer에 비해 훨씬 퍼포먼스 부담 적음