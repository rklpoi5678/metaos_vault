## 코드 리뷰를 위한 좋은 Commit 만들기
Pull Request와 마찬가지 좋은 커밋도 이해하기 쉽고 명확해야한다. 

**좋은커밋이란?**
1. 의미 있는 단위의 작업해야 할 것
	1. 한 개 커밋이 하나의 기능이나 작업을 완성해야 좋은 커밋이다. 작게 유지하지만 너무 작은 커밋을 하는것은 다량의 커밋을 양산할뿐 좋은 커밋이라 하긴어렵다.
	2. 이 의미있는 단위는 조직에서 정해 주는 경우, 암묵적인 합의로 존재하는 경우, 어떤것이든지 동료들이 사용하는 단위를 크게 벗어나지 않게 작업하는 것을 권장한다.
2. 생성된 커밋은 동작이 가능한 형태여야함
	1. 프로젝트 전체 동작을 방해하지않는지... 이런 검증 작업은 자동화하기도 한다.
	2. 복잡하거나 구조상 이유로 자동화 테스트를 하기 어려운경우 수동 테스트를 통해 커밋의 동작을 검증한다.
3. 커밋 메시지는 명확하고 간결하게 작성
	1. 그 자체로도 커밋의 의미를 명확하게 전달해야함, Conventional Commit이라는 커밋 메시지 규칙이 있다.
	2. `<type>(<scope>): <subject>`의 형식을 따르게 된다. 여기서 type은 커밋의 종류를, scope는 커밋의 영향을 미치는 범위를 subject에는 커밋의 간햑한 설명을 적는다.
	3. 새로운 기능을 추가했다면 `feat(UserProfile): Add email verification`과 같이 작성할 수 있습니다. 이는 'UserProfile'영역에 '이메일 확인'기능을 추가했다는 것을 명확하게 알린다.
	4. -> 이러한 방식으로 커밋 메시지를 작성한다면 다른 개발자들이 변경 사항을 빠르고 쉽게 이해할 수 있다.

## type
feat: 기능 개발과 관련
docs: 주석/ReadMe 등 문서화 관련
test: 테스트 관련
fix: 버그나 type등 수정 사항 관련
chore: 코드와 관련이 없는 내용들을 수정할 때 (License등)
ci: CI/CD 등과 관련한 작업을 수행할때

> feat type을 가진 커밋 메시지를 모아서 Release Note등을 자동으로 생성할수있다.

! 이규칙은 엄격하지않다. 이 규칙을 따를필요도 없다. 변형해서 사용할수있다. 꼭 영어로만 써서 해야되는것도 아니다. 일종의 가이드라인이다.

## 자동으로 style 맞추기: Linting
**자동으로 규칙 체크하기**
개발자들은 자동화를 좋아한다. 규칙을 외우고 적용하는 불편함을 그냥 보고 넘길리없다.(Linting이 등장) 자동으로 체크하는기능, 언어에 따라 린팅을 맞춰 사용한다.

링틴외에 Formatter가있는데, Linting툴이 작성된 코드의 규칙 위반 여부를 검사만 한다면, Formatter는  Linting에 맞도록 자동으로 코드를 바꿔준다.
스타일 가이드에 맞춰주기에 개발자들은 스타일을 고민할 필요 없이 로직에만 집중할수있다.

## Linting 툴을 사용하면 어떤 효과를 볼까?
- 팀 전체 동일한 코딩 스타일을 유지
- 코드 가독성, 이해하기 쉽게 만든다.
- 핵심 로직에만 집줍하게 만들수 있다.

## Git을 사용해 팀원간 린팅 규칙 통일하기
설정 파일로 부터 자동으로 린팅이 설정되게 할수있다.
이러한 설정 파일을 Git으로 공유하면 모두가 손쉽게 Linting을 설정할 수 있다.

## 실습
**JS경우**
ESLint와 Prettier을 사용한다. ESLint는 Linter로서, Prettier는 Formatter로서 작동한다.

적용전(극단적인 예시)
```js
const name="John", age=25, message='Happy birthday!' ; const arr=[1,2,3,4,5]; const...
```

적용후(Formatter를 적용함)
```js
const name = 'John',
  age = 25,
  message = 'Happy birthday!';
const arr = [1, 2, 3, 4, 5];
const day = 'Monday';
function greet(name, age) {
  const message = 'Hello, ' + name + '. You are ' + age + ' years old.';
  console.log(message);
}
if (day == 'Monday') {
  console.log('Today is Monday.');
} else if (day == 'Tuesday') {
  console.log('Today is Tuesday.');
} else {
  console.log('Today is not Monday or Tuesday.');
}
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
greet(name, age);
```

## ESLint
JavaScript의 Linting 도구이다. ESLint는 플러그인을 통해 React, Vue등과 같은 프레임워크나 라이브러리에 맞는 특화된 규칙을 추가할수있다.
프로젝트 루트에 `.eslintrc`파일을 생성하고 ESLint옵션을 추가할 수 있다.
```js
{
	"root": true,
	"extends": ["eslint:recommended", "plugin:@typescript-eslint/recommended"]
	"ignorePatterns": ["src/**/*.test.ts", "src/frontend/generated/*"]
}
```
root레벨에 있는 ESLint 설정 파일임을 나타내고
ESLint의 규칙인 `eslint:recommended`와 TS를 위한 규칙인 `plugin:@typescript-eslint/recommended`를 사용하도록 설정, 또한 테스트와 생성된 파일들을 Linting에서 제외하고 있다.
```bash
# 다음 두가지 명령 중 선택해서 사용할 수 있다.
npx eslint yourfile.js
yarn run eslint yourfile.js
```
CLI로 interactive하게 Linting을 설정할수도 있다.
```bash
npx eslint --init
```
![[Pasted image 20250819233147.png]]

## Prettier
코드 포매팅에 초점을 맞춘 도구이다. JS뿐 아니라 TS,CSS,HTML등 다양한 언어를 지웒나다. 프로젝트 루트 하위에 `.prettierrc`파일에 Prettier옵션을 추가할 수 있습니다.
```.prettierrc
{
	"trailingComma": "es5", #(1)
	"tabWidth": 2,          #(2)
	"semi": true,           #(3)
	"singleQuoto": true     #(4)
}
```
- (1): ES5에서 지원하는 위치에서 코드 뒤에 콤마를 추가
- (2): 탭의 너비를 2 스페이스로 설정
- (3): 문장 끝에 세미콜론을 사용한다.
- (4): 문자열을 표시할 때 단일 따옴표를 사용한다.
```bash
# 이 또한 두 명령 중 선택해서 사용할 수 있다.
npx prettier --write yourfile.js
yarn run prettier --write yourfile.js
```

## 주의
ESLint와 Prettier는 서로 충돌할수있다.
이를 방지하기 위한 플러그인을 설치해줘야한다.
```bash
npm install eslint-config-prettier eslint-plugin-prettier --save-dev
```

## Python의 경우
매우 다양한 린팅이 존재
1. 동적언어여서
2. 생태계가 다양해서
3. Flake8, Black, isort, Pylance 등의 Linter/Formatter등
