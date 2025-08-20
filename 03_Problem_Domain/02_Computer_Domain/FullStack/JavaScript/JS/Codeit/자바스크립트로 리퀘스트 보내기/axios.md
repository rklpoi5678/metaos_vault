## axios 문법
```js
export async function getColorSurveys(params = {}) {
	const url = new URL('https://...');
	/*
	 예를 덜어
	 params에 { offset: 5, limit: 10}; 이 전달된다면
	 url.searchParams에 offset은5 limit은 10이 추가되는것이다.
	 */
	Object.keys(params).forEach((key) => {
		url.searchParams.appned(key, params[key])
	});
	
	const res = await fetch(url);
	const data = await res.json();
	return data;
}

export async function getColorSurvey(id) {
	const res = await fetch(`../${id}`)
	const data = await res.json();
	return data;
}

export async function createColorSurvey(survay) {
	const res = await fetch('...',{
		method: 'POST',
		body: JSON.stringify(surveyData),
		headers: {
			'Content-Type': 'application/json',
		},
	});
	const data = await res.json();
	return data;
}
```
> axios.get, axios.post patch엔 두번째인자로 원하는 값을 주기만하면 axios가 알아서 해석한다.ㅐ

```js
import axios from 'axios';

const instance = axios.create({
	baseURL: '...',
	timeout: 3000,
});

export async function getColorSurveys(params = {}) {
	const res = instace.get('/color-survey', {
		params	
	});
	return res.data;
}

export async function getColorSurveyt(id) {
	const res = instace.get(`/color-survey/${id}`); 
	return res.data;
}

export async function createColorSurvey(surveyData) {
	const res = instace.post('/color-survey',surveyData)	
	return res.data;
}
```

## axios 오류 처리하기
오류를 처리하기 편해진다. (에러 상태코드를 axios가 자동으로 관리해준다.)
일반 try-catch로 감싸줘도된다.
```js
const surveyData = {
	mbti: 'ESFJ',
	password: '0000',
};

try {
	const survey = await getColorSurvey(surveyData);
	console.log(survey);
} catch (e) {
	console.log('오류가 발생했습니다.')
	console.log(e.response); // axios는 자동으로 에러를 객체에담아준다.
	//console.log(e.response.status);
	//console.log(e.response.data);
}
// response가 돌아와야지만 리스폰스객체가 존재함
// ..그러므로 status,data는 일단 리스폰스객체가 들어와야 찍히기때문에 그여부를 확인하는게 좋다.
.. catch(e) {
	if(e.response) {
		console.log(e.response.status);
		console.log(e.response.data);
	} esle {
		console.log('리퀘스트가 실패했습니다');
	}
}

```

## 정리
axios는 HTTP메소드 이름과 동일한 메소드를 사용하고 리스폰스 바디에 data프로퍼티로 접근가능
```js
//get request

// axios
async function getColorSurvey(id) {
  const res = await axios.get(`https://learn.codeit.kr/api/color-surveys/${id}`);
  return res.data;
}

// fetch
async function getColorSurvey(id) {
  const res = await fetch(`https://learn.codeit.kr/api/color-surveys/${id}`);
  const data = await res.json();
  return data;
}

// query parameter로 보낼경우 params옵션

// axios
export async function getColorSurveys(params = {}) {
  const res = await axios.get('https://learn.codeit.kr/api/color-surveys', {
    params,
  });
  return res.data;
}

// fetch
async function getColorSurveys(params = {}) {
  const url = new URL('https://learn.codeit.kr/api/color-surveys');
  Object.keys(params).forEach((key) =>
    url.searchParams.append(key, params[key])
  );
  const res = await fetch(url);
  const data = await res.json();
  return data;
}
```

```js
// axios 인스턴스
const instance = axios.create({
  baseURL: 'https://learn.codeit.kr/api',
  timeout: 3000,
});

async function getColorSurveys(params = {}) {
  const res = await instance.get(`/color-surveys`, {
    params,
  });
  return res.data;
}

/**
`axios`는 리퀘스트 자체가 실패하거나 리스폰스의 상태 코드가 실패(4XX, 5XX)를 나타내면 Promise를 reject 합니다.
*/
```