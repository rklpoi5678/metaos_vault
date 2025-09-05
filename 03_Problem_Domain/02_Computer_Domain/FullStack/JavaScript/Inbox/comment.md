## 핵심
```javascript
// 한줄 주석

/**
* 두 줄 이상
* 주석
*/
```
JSDoc: 자바스크립트 API문서 생성기. 자바스크립트 소스코드에 JSDoc형식의 주석을 추가하면 API를 설명하는 HTML문서를 생성할수있다.
(함수의 기능,파라미터,return값 에 대한 설명, 해당 함수를 사용할 때 작성한 정보를 표시해줄 수 있다.)

자바스크립트로 코드를 작성하면 모든 타입이 any로 추론된다. 그래서 어떤 타입의 데이터를 파라미터로 넘겨야 하는지 알려면 함수 선언부에 가서 작성된 주석을 보거나 코드를 직접해석해야 한다.

```JavaScript

/**
* a와 b를 더한 결과를 반환
* @param {number} a 첫번째 숫자
* @param {number} a 첫번째 숫자
* @return {number} a와 b를 더한 결과
*/

function plus(a,b) {
	return a + b;
}
```
@는 파라미터, @return은 리턴 데이터에 대한 설명을 적을 수 있는 태그이다.

\[태그유형] \{타입} 변수명 설명 순으로 작성


```JavaScript
//#regin 숫자 계산 함수
/**
* 
* ~~~
*/
functon ~~
/**
* 
* ~~~
*/
functon ~~
//#endregin
```
region 주석은 코드를 묶어주는 기능을 한다.
코드를 묶을 시작점에서 //#region 설명을 작성해주고, 끝나는 지점에서 //#endregion을 작성하면 된다.

```JavaScript
/** @type {string} 닉네임 */
let nickname = '';
/** @type {string} 이메일 */
let email = '';
/** @type {string} 비밀번호 */
let password = '';
```
변수에 대한 설명을 통해 어떤 데이터를 넣어야할지 알 수 있게 된다. 또한 향후 이 예제에 나온 파라미터를 쓸때

```JavaScript
async function onClickRegister(nickname, email,password) {
	...
}
```
일때
```js
/**
 * 회원가입 클릭 이벤트. 회원가입 결과 콘솔에 출력
 * @param {string} nickname 닉네임
 * @param {string} email 이메일
 * @param {string} password 비밀번호
 */
```
위와 같은 주석을 넣어 파라미터도 어떤 자료형을 넣어줘야 할지 바로 알수있게한다.

나중에 혹은 다른 개발자가 파일을 열었을 때 어떤 코드들이 작성되어 있는지 한눈에 파악하기 어렵다.
-> \#region 주석으로 그룹화하기

## 예제
```js

//#region 변수
/** @type {string} 닉네임 */
let nickname = '';
/** @type {string} 이메일 */
let email = '';
/** @type {string} 비밀번호 */
let password = '';
//#endregion

//#region 이벤트
/**
 * 회원가입 클릭 이벤트. 회원가입 결과 콘솔에 출력
 * @param {string} nickname 닉네임
 * @param {string} email 이메일
 * @param {string} password 비밀번호
 */
async function onClickRegister(nickname, email, password) {
  if (!isValidNickname(nickname)) {
    console.log('Invalid nickname');
    return;
  }
  if (!isValidEmail(email)) {
    console.log('Invalid email');
    return;
  }
  if (!isValidPassword(password)) {
    console.log('Invalid password');
    return;
  }
  const response = await register(nickname, email, password);
  console.log(response);
}
//#endregion

//#region 함수
/**
 * 회원가입 처리
 * @param {string} nickname 닉네임
 * @param {string} email 이메일
 * @param {string} password 비밀번호
 * @returns {Promise<string>} 회원가입 결과 메시지
 */
async function register(nickname, email, password) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Register Successful!');
    }, 2000);
  });
}

/**
 * 닉네임 유효성 검사
 * @param {string} nickname 닉네임
 * @returns {boolean} 유효성 검사 결과
 */
function isValidNickname(nickname) {
  return /^[가-힣]+$/.test(nickname);
}

/**
 * 이메일 유효성 검사
 * @param {string} email 이메일
 * @returns {boolean} 유효성 검사 결과
 */
function isValidEmail(email) {
  return /[a-z0-9]+@[a-z]+\.[a-z]{2,3}/.test(email);
}

/**
 * 비밀번호 유효성 검사
 * @param {string} password 비밀번호
 * @returns {boolean} 유효성 검사 결과
 */
function isValidPassword(password) {
  return /^[a-z0-9_-]{6,18}$/.test(password);
}
//#endregion
```
