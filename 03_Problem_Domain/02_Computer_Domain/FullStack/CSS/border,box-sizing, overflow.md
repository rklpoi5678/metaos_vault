## 핵심
border
```CSS
/* 박스에 선을 줄수있다 굵기, 선의종류(대시 , emdash,점대시등등), 선색상 */
border: 1px soild #fbfbfb

/* 박스 모서리의 곡선을 줄수있으며 이것을로 동그란 박스를 만들수있다. */
border-radius: 36px 
border-radius: 9999px /* 이렇게 큰값을 지정하면 알약형태ㄱ */

/* 퍼센트 사용 */
border-radius: 50% /*50%만큼 둥글게 이러면 타원형태가 된다.*/
```


## box-sizing
기본적으로 테두리,보더 값과 컨텐츠값을 합친값을 기본으로 사이즈가 계산된다.
총 너비: (콘텐트) + 2(왼쪽 오른쪽) * (패딩 + 보더)

그럴땐 box-sizing: border-box면 border사이즈 기준으로 한다. 요즘은 이것이 편해서 현대적인 프로그래밍에서는 일단 넣고 본다.
```CSS
* {
 box-sizing: border-box;
}
```

## overflow
요소안에 글자가 외곽으로 뛰어나가는 현상을 오버플로우라고 하며 숨기거나, 숨긴내용을 스크롤로 보여줄수있게 하거나 가로스크롤을 시킬수있게 해준다.

```CSS
overflow: hidden;
overflow: scroll;

/* wrap */
/*
	기본적으로 CSS에서 적용해주는 줄바꿈을 적용하지 않겠다면 nowrap을 사용한다.
*/
white-space: nowrap;
```
줄바꿈을 하지않게 되면 가로로 넘치게되겠죠?(오버플로우) 그것을 오버플로우 scroll 속성을 넣어주면 가로로 스크롤 되겠죠