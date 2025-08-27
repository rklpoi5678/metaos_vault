## 핵심
누산기
```js
const addNum ((acc,cnt) => {
	return acc += cnt	
},초기값)
```

객체
```js
const arr = [1,2,3,4,5,6];

let result = arr.reduce((acc,cnt) => {
	console.log(
		`인덱스:${i}, 누산기:${acc}, 현재원소: ${} 원본 배열: ${}`	
	)
})
```

깊은복사
strucutredClone()