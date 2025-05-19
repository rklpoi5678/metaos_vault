## 상태: user,handleLogout,setUser -> useAppStore()에서
## isMobileMenuopen, setIsMobileMenuopen -> useState(false)
(모바일 메뉴 상태 -> 초기값은 접은상태)

user,setUser상태가 변할때마다
로컬스토리지에 `isLoggedIn`을 담고
유저가 아니거나 && 유저일때 setUser상태를 null로

헤더바 로고 -> 다시메인페이지로
about,blog,pdf-generator로 분기

md:hidden 일때 모바일에서 햄버거 모양
모바일 상태(사이드바 관련)
로그인 상태 일시 (PC동일) 대시보드 로그아웃 표시로 바뀜

로그아웃시 (handleLogout 이벤트시)
로컬 + Supabase.auth.SignOut() -> user상태를 null로
