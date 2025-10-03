## 핵심
사진,버튼,글 상자 등을 어떤 규칙으로 어디에 놓을지 정하는것이다.
원래 있던 자리에 놓을지, 아니면 특별히 움직여서 띄울지 등을 결정하는것이다.

## 사용성
웹 모든 요소는 기본적으로 static이라는 포지션을 가진다. 이는 HTML코드에 쓰인 순서대로 화면에 차례대로 배치된다는 뜻이다. 하지만 때로는 특별한 위치에 놓고 싶을때가있다.
- 단순히 margin이나 padding만으로는 한계가 있다.
- 테일윈드는 css의 position속성을 사용해서, 요소의 배치 방식을 쉽게 제어할 수 있게해준다.

## position클래스 사용법
- static: 기본값, 원래 HTML 코드에 작성된 순서대로 일반적인 흐름에 따른다. top,bottom,left,right 같은 속성은 이 클래스에 영향을 주지않는다.
```HTML
<div class="static bg-gray-200 p-2">나는 원래 자리에 있다.</div>
```
- relative: static으로 배치될 자리에 일단 놓이는데 그 자리에서 top,bottom,left,right 같은 속성을 사용해 미세하게 위치를 움직일수있다. 움직여도 원래 차지한 공간은 여전히 비워둔다.즉, 다른 absolute요소의 기준점이 될 때도 많이 쓰인다.
```HTML
<div class="relative top-4 left-4 bg-blue-200 p-2">
	나는 원래 있던 자리에서 오른쪽 아래로 4px 움직였어요.
</div>
```
- absolute: 요소는 원래 웹 페이지의 흐름에서 완전히 '떨어져 나와'자유롭게 움직인다. top,bottom,left,right 속성을 사용해 위치를 지정하는데, 이때 가장 가까운 relative,absolute,fixed,sticky 포지션을 가진 '부모 요소'를 기준으로 움직인다. 만약 그런 부모 요소가 없다면 \<body> 태그를 기준으로 움직인다. 이 요소는 공간을 차지하지 않는다.
```HTML
<div class="relative w-48 h-48 bg-gray-300 p-4">
	<button class="absolute top-0 right-0 bg-red-500 text-while p-1">
		닫기
	</button>
</div>
```
- fixed: 화면(뷰포트)의 특정 위치에 '고정'되어 절대 움직이지 않는다. 스크롤해도 항상 그 자리에 머문다. 주로 상단 메뉴바, 하단 푸터 바, 스크롤 버튼 등에 사용되며, 이 요소도 공간을 차지하지 않는다.
```HTMl
<nav class="fixed top-0 left-0 w-full bg-black text-white p-4">
	나는 화면 상단에 항상 고정되어 있다.
</nav>
```
- sticky: 기본적으로 relative처럼 동작하다, 특정 스크롤 위치에 도달하면 fixed처럼 '고정'되는 하이브리드 방식이다. 예를 들어, 목차가 스크롤되다가 화면 상단에 닿으면 거기 고정되어 더이상 스크롤되지 않는 식이다.
예1:
```HTML
<div class="sticky top-0 bg-yellow-200 p-2 z-10">
	나는 스크롤하다가 화면 상단에 닿으면 고정됀다!
</div>
```
예2:
<div> 
	<div>
		 <div class="sticky top-0 ...">A</div>
		  <div> 
			  <div> 
				  <img src="/img/andrew.jpg" />
				   <strong>Andrew Alfred</strong>
				</div> 
			<div> 
				 <img src="/img/aisha.jpg" /> 
				 <strong>Aisha Houston</strong> 
			</div> 
			<!-- ... --> 
			</div> 
			</div> 
			<div> 
			<div class="sticky top-0">B</div> <div> <div> <img src="/img/bob.jpg" /> <strong>Bob Alfred</strong> </div> <!-- ... --> </div> </div> <!-- ... -->
	
</div>

## 정리
position 유틸리티는 staic, relative, absolutem fixed, sticky 같은 간단한 클래스를 사용해서, 웹 페이지 요소들이 어떤 방식으로 화면에 배치되고 움직일지 아주 쉽게 제어하는 기능이다.

복잡한 레이아웃을 만들거나 특정 화면을 화면에 고정시키는 등 다양한 시각적 효과를 구현한다.