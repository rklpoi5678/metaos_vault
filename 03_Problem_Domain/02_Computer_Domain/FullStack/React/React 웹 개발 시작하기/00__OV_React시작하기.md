## 프로젝트 생성
```bash
# create-react-app으로 리액트 프로젝트생성
npm init react-app <filder name>
# 혹은 폴더를 VS Code로 열고 터미널에서
# npm init react-app .
```
> 개발 모드 실행 npm run start
> 개발 모드 종료 Ctrl + C
> Create React App(CRA)은 더이상 관리되지 않는 프로젝트이기 때문에, 프로젝트 생성엔 Vite라는 도구를 쓰는것을 권장한다.

```bash
npm create vite@latest . -- --template react

# after
npm install

# 개발 환경 테스트
npm run dev
# npm run start // 프로덕션 용
```


## 리액트 개발자 도구 살펴보기
React Developer Tools(리액트용 개발자 도구)
App은 리액트에서 가장 기본적인 컴포넌트이다.

## React v18 이후 문법
```js
import ReactDOM from 'react-dom/client';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<h1>안녕 리액트!</h1>)
```
> ReactDOM.createRoot()를 사용해서 root를 만든다음 root.render로 사용한다.

리액트에서 기본적으로 시작은 index.html부터 시작한다.

index.html이후 main.jsx가 시작된다. 리액스 코드중에서 가장 먼저 실행되는 코드이다.