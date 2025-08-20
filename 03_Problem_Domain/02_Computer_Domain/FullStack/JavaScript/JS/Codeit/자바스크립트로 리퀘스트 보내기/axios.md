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