핵심
`animation, @keyframes`


## @keyframs 란?
키프레임이란 CSS 스타일이 변화되는 중간 지점을 의미한다. 어떤 시점에 요소가 스타일을 가져야 하는지 단계별로 정의할수있는것

문법
1. 처음 스타일과 최종 스타일을 정하는것
```CSS
@keyframes animation-name {
	from {
		/* 처음 스타일 */
	}
	to {
		/* 최종 스타일 */
	}
}
```
2. 좀 더 세분화해서 단계별로 정의하는 방법
```CSS
@keyframes animation-name {
	0% {
		/* 처음 스타일 */
	}
	50% {
		/* 중간 스타일 */
	}
	100% {
		/* 최종 스타일 */
	}
}
```
사용법
animation-name, animation-duration 사용해도되고
animation으로 한번에 줘도된다.
```CSS
.box {
	animation-name: animation-name;
	animation-duration: 3s;
}
```
```CSS
.box {
	animation: animation-name 3s;
}
```

animation-delay
애니메이션이 시작되기 전 기다리는 시간을 설정한다.