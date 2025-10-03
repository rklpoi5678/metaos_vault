## 핵심
이 사진은 혼자 크게 배치할까? 아니면 다른 사진이랑 옆으로 나란히 놓을까? 아예 숨길까?
사진의 배치 방식을 정하는것이다. 웹 페이지의 모든 요소(사진,글,버튼 등) 화면에 어떻게 '보여지고 배치될지'를 결정하는 아주 기본적인 규칙이다.

## 디스플레이의 중요성
HTML요소는 기본적으로 화면에 보여지는 방식이 정해짐, 어떤 요소는 혼자 한 줄 차지(블록), 어떤 요소는 다른 요소 옆에 나란히 놓이고(인라인), 어떤 요소는 특정 규칙에 따라 자유롭게 움직이기도 한다.
- 문제는 기본적으로 HTML 요소들은 정해진 `display`값을 가진다. `div,p`는 기본적으로 `display:block;`이라서 항상 새로운 줄에서 시작, 혼자 한줄을 다 차지한다., 반면 `span,a`는 `display: inline`이라 자기 내용만큼만 공간을 차지하고 옆으로 나란히 배치된다.
- 그럼 `div옆div`를 나란히 놓을려면 CSS의 display 속성을 직접 변경해야했다.
```CSS
.my-div {
	display: inline-block; /* div를 인라인 처럼 옆에 놓으면서 블록처럼 크기 조절 가능*/
}
.my-span {
	display: block; /* span은 한 줄 차지하게 만듦*/
}
```
> 반복하지만 CSS 파일을 왔다 갔다 해야 하고, 클래스 이름도 지어줘야 하는 번거로움이 있었다.

해결책: display속성을 유틸리티 클래스로 제공해서 아주 간단하게 제어할 수 있게 해준다. HTML 태그 안에 block,inline,flex,grid 등 원하는 디스플레이 타입에 해당하는 클래스만 넣어주면 된다.
```HTML
<div class="block">이 div는 항상 한 줄차지</div>
<span class="inline">이 span는 옆으로 나란히 놓을수있다.</span>

<div class="inline-block">인라인 블록</div>
<div class="inline-block">또 다린 인라인 블록</div>
```

## 디스플레이 유틸리티 사용법 (사진 배치 방식 정하기)
- block: 요소를 블록 레벨 요소로 만들기, (div,p 기본값)
```HTML
<p class="block">이 문단은 한 줄을 혼자 다 차지합니다.</p>
```
- inline: 요소를 인라인 레벨 요소로 만든다. 내용물 만큼만 공간차지, 다른 인라인 요소 옆에 나란히 배치가능(span,a 기본값)
```HTML
<span class="inline"> 인라인 텍스트 </span>
<span class="inline"> 옆에 붙습니다. </span>
```
- inline-block: 인라인 레벨이면서 동시에 블록처럼 동작, width,height,padding,margin 등을 블록 요소처럼 자유롭게 지정할 수 있다.
```HTMl
<div class="inline-block w-32 h-32 bg-blue-200">상자 1</div>
<div class="inline-block w-32 h-32 bg-green-200">상자 2</div>
```
(이 두 상자는 옆으로 나란히 배치되면서, 각각 너비와 높이를 가질수있다.)
- flex: 요소를 플렉스 컨테이너로 만든다. 이 요소의 자식들은 플렉스박스 규칙에 따라 유연하게 정렬되고 배치될 수 있다. (현대 웹 레이아웃에서 가장 많이 사용)
```HTML
<div class="flex justify-between items-center"> <span>왼쪽</span>
	<span> 오른쪽 </span>
</div>
```
- inline-flex: flex와 비슷하지만, 인라인 레벨의 플렉스 컨테이너 이다. 다른 인라인 요소 옆에 나란히 놓일 수 있다.
```HTML
<div class="inline-flex space-x-2"> 
	<button>버튼 1</button>
	<button>버튼 2</button>
</div>
```
- grid: 요소를 그리드 컨테이너로 만든다. 이 요소들의 자식 요소들은 그리드 시스템에 따라 행과 열에 맞춰 배치될 수 있다.
```HTMl
<div class="grid grid-cols-3 gap-4"> <div>아이템 1</div>
	<div>아이템 2</div>
	<div>아이템 3</div>
</div>
```
- inline-grid: grid와 비슷하지만, 인라인 레벨의 그리드 컨테이너예요
- table: 요소를 CSS테이블 처럼 동작하게 만들어요(\<table>태그처럼)
- table-row: CSS 테이블 행처럼 동작해요 (\<tr>태그처럼)
- table-cell: CSS 테이블의 셀처럼 동작해요. (\<td>,\<th>태그처럼)
	- 이 세 가지는 HTML의 실제 `<table>`태그 대신 일반 `div`등으로 테이블 구조를 만들 때 사용해
- hidden: 요소를 완전히 숨겨서 화면에 보이지 않고, 공간도 차지하지 않게 만든다. (css: display: none;과 동일)
```HTML
<div class="hidden">이 내용은 화면에 보이지 않아요.</div>
```

## 반응형 디자인과 결합 (화면 크기에 따라 배치 방식 바꾸기)
물론 md:, lg: 같은 반응형 접두어를 함께 사용하여 화면 크기에 따라 디스플레이 방식을 다르게 설정할 수 있다.
```HTML
<div class="block md:flex lg:grid"> </div>
```
" 스마트폰에서는 사진을 세로로 한 장씩 보여주고, 태블릿부터는 옆으로 나란히, 데스크톱 부터는 격자 모양으로"

## 정리
display 유틸리티는 block,inline,inline-block,flex,grid,hidden 등 간단한 클래스를 사용해서 HTML요소가 화면에 어떻게 보여지고 배치될지를 아주 직관적이고 유연하게 제어할 수 있게 해주는 핵심이다.