## 핵심
지도위 요소를 원하는 기준점에서 얼마나 떨어뜨려 놓을까 정하는것과 같다.
위에서 얼마, 오른쪽에서 얼마, 이렇게 정확한 위치를 지정해 주는 지시이다.

이 클래스는 position 속성과 함께 사용할때 빛을 발한다.

css에서 요소를 정확한 위치에 놓으려면 position 속성을 지정한 다음, top: 20px;, left: 50%; 이런 식으로 각 방향별 위치 값을 따로 써야했다.
```CSS
.my-element {
	position: absolute;
	top: 20px;
	right: 10px;
}
```
CSS 파일을 계속 수정하며, 반응형 디자인을 만들때는 미디어 쿼리 안에 또 이 값을 바꿔야 하니 여러모로 불편하다.

테일윈드는 top,right,bottom,left 속성을 유틸리티 클래스로 제공해 HTML안에서 바로바로 요소의 위치를 조절할 수 있게 해준다.

## 사용법
- top-0,right-0,bottom-0,left-0 : 해당 방향으로 0px 떨어뜨려 놓아 딱 붙게 만든다.
```HTML
<div class="relative w-48 h-48 bg-gray-300">
	<button class="absolute top-0 right-0 gb-red-500 text-white">
		닫기
	</button>
</div>
```
- top-4,bottom-8,left-px 등: 테일윈드의 간격 스케일에 따라 요소를 해당 방향으로 떨어뜨려 놓는다.
```HTML
<div class="relative w-48 h-48 bg-gray-300">
	<span class="absolute top-4 left-4 bg-blue-500 text-white p-1">
		알림
	</span>
</div>
```
- 음수값 : 요소를 반대 방향으로 밀어내거나 겹치게 만든다.
```HTML
<div class="relative w-48 h-48 bg-gray-300">
	<div class="absolute -top-4 left-1/2 -translate-x-1/2 bg-green-500 rounded-full w-8 h-8"></div>
</div>
```
- 퍼센트 값: 부모 요소 크기에 대한 퍼센트로 위치를 지정할 때 사용
```HTML
<div class="relative w-full h-64 bg-gray-200">
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 bg-blue-500 w-24 h-24">
        </div>
</div>
```
- 모든 방향(inset-0, inset-y-0, inset-x-0): y축 = top,bottom, x축=left,right 으로 한 번에 값을 지정할 수 있는 단축 클래스
	- inset-0: top-0 right-0 bottom-0 left-0 와 같아서, 부모 요소에 꽉 채운다.
	- inset-y-0: top-0, bottom-0 와 같아서 , 세로 방향으로 꽉 채운다.
	- inset-x-0: left-0,right-0 와 같아서, 가로 방향으로 꽉 채운다.

## 정리
해당 유틸리티는 position 속성(absolute, fixed, sticky, relative) 적용된 요소들을 기준점에서 원하는 거리만큼 정확하게 배치할 수 있게 해주는 도구이다.