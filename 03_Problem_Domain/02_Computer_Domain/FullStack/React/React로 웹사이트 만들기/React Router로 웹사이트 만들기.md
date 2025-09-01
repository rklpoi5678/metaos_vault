html을 사용하면 페이지마다 여러 html을 사용하면된다. 그러나 리액트에서는 모든것을 컴포넌트로 효율적으로 만들기 위함 다양한 방법중  ReactRouter을 많이사용한다.

## 리액트 라우터 v6소개
리액트 컴포넌트로 페이지를 나누는 라이브러리
```jsx
//ex: 페이지 나누기
<Routes>
	<Route path="/" element={<HomePage />} />
	<Route path="courses" element={<CourseListPage />} />
	<Route path="courses/1" element={<CoursePage />} />
	<Route path="*" element={<NotFoundPage />} />
</Routes>

// 핵심 컴포넌트
<Link to="/">홈페이지</Link>
<Link to="/courses">수업 탐색</Link>
<Link to="/questions">커뮤니티</Link>

// 이외에도 Router,Routes,Route, Link
```

**Router**
이것이 없으면 리액트 라우터를 쓸수없다. 내부적으로 Context Provider이다.
ReactRouter기능을 사용하려면 라우터 안에서 사용해야한다.
```jsx
import { BrowserRouter } from 'react-router-dom';

// 이렇게 전체를 감싸면 리액트라우터를 프로젝트 전체에 쓸수있게해줄수있다.
function Main() {
	return <BrowserRouter> ... </BrowserRouter>;
}

export default Main;
```
**Routes, Route**
```jsx
// 해당 주소를 찾아 한줄씩보고 맞다면 해당 컴포넌트를 보여준다.
<Routes>
	<Route path="/" element={<HomePage />} />
	<Route path="courses" element={<CourseListPage />} />
	<Route path="courses/1" element={<CoursePage />} />
	<Route path="*" element={<NotFoundPage />} />
</Routes>
```
**Link**: a태그처럼 사용하는것

