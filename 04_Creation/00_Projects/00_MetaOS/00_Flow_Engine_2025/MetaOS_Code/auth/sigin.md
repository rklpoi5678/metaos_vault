## 'useClient'
Supabase사용 
hydration 문제 -> intersectioin-observe 사용
shadn/ui 컴포넌트인 Button/input/Card 사용
Zustand의 useUserStore사용

이메일,패스워드,메시지 기본값('') 없는 상태로 설정
로딩 기본값(false)상태

로컬 스토리지로 저장된 로그인 상태가 'true'이면
바로 /dashboard 이동 \[\router] 들어올때마다

로그인 버튼 클릭시(handleLogin)
-> 로딩상태(true)변경 -> 메세지('')설정
->Supabase(siginWithPassword)의 이메일,비밀번호
->error시 (supabase에서 보내온신호)->에러메시지 OR '로그인~'(에러시)

-> 로컬스토리지에 로그인 상태 true로 메시지("로그인성공!") 표시
->router.push('/dashboard')

## 디자인
로딩상태가 true일시 보여주는 디자인이존재
sumit시 React.FormEvent -> handleLogin 발동
