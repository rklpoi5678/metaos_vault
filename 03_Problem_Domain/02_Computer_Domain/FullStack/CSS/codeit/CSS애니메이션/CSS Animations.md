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
애니메이션이 시작되기 전 기다리는 시간을 설정한다. 즉, 애니메이션을 일정 시간 동안 지연시키는것이다.
```CSS
.box{
	animation-delay: 1s; /* 1초 있다가 실행이된다. */
}
```

animation-iteration-count
```CSS
.box1 {
	animation-iteration-count 3: /* 3회 반복후 애니메이션 정지 */
}
.box2 {
	animation-iteration-count: infinite; /* 무한 반복을 한다. */
}
```

animation-timing-function
transition에서 배웠던 베지에 곡선을 지정한다. ease,linear,ease-in-out등의 값들을 사용
```CSS
@keyframes change-length {
	form {
		transform: scaleX(1);
	}
	to {
		transform: scaleX(3);	
	}
}

.box {
...
	animation-name: change-length;
	animation-duration: 3s;
	animation-iteration-count: infinite;
	transform-origin: left;
}


.box0 {
	animation-timing-function: ease;
}
.box1 {
	animation-timing-function: linear;
}
.box2 {
	animation-timing-function: ease-in;
}
```

animation-direction
애니메이션의 재생방향을 정한다. 기본값normal(순방향),reverse(역방향)으로 애니매이션 재생
alternate는 순방향시작 순방향과 역방향을 번갈아 재생, 그리고 alternate-reverse는 역방향으로 