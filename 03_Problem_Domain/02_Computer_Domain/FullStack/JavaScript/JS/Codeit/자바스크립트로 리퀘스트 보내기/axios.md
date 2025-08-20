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