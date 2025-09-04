##  핵심
`*.module.css`의 의미
- css Modules라는 기능을 쓰겠다는 표시이다.
- css Modules는 **클래스 이름을 컴포넌트 단위로 "자동으로 고유화" 해준다.**
- 이렇게 하면 전역 CSS처럼 클래스 이름이 충돌하는 문제를 막을수있다.
```jsx
.title {
	color: red'	
}
```
```jsx
import './ColorSurvey.css';

export default function ColorSurvey() {
	return <h1 className="title">title</h1>;
}
```
##  CSS Module 
```jsx
/* ColorSurvey.module.css*/
.title {
	color: red;
}
```
```jsx
import styles from './ColorSurvey.module.css';

export default function ColorSurvey() {
	return <h1 className={styles.title}>Hello</h1>;
}
```
- 빌드시  .title이 ColorSurvey_title__3XyZ1 같은  고유한 이름으로 변환됨
- 다른 컴포넌트의 .title과 절대 충돌하지 않음
- styles.title처럼 객체 프로퍼티로 접근해야 함

## 왜 중요한가?
- 규모가 커질수록 -> CSS클래스 이름 충돌은 흔한 문제
- CSS Modules를 쓰면 **컴포넌트 단위 스타일 캡슐화**가 가능해져서 유지보수가 쉬워집니다.
- 특히 팀 프로젝트나  디자인 시스템에서 안전하게 스타일을 관리할 수 있다.
---

"이 CSS는 이 컴포넌트 전용으로 안전하게 쓸 거야"라는 약속이다.
 그래서 React + CRA, Next.js 같은 환경에서는 .module.css 네이밍이  규칙처럼 자리 잡았다.
 
 ---


 