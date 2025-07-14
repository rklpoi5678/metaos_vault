## 핵심
기본적으로 얼마만큼의 '시작 공간'을 차지할지 미리 정해주는 것이다.
물건들이 늘어나거나 줄어들기 전에, 각자 얼마의 공간에서 시작할지 미리 정하는 것이다.

## 왜?
요소들을 유연하게 배치하는데 강력하기 떄문이다. flex컨테이너 안 자식요소들은 공간이 남으면 늘어나고, 공간이 부족하면 줄어든다.
flex-basis는 이런 늘어나고 줄어들기 전에 각 아이템이 기본적으로 가져야할 너비 높이를 지정
- css에서 지정시 flex-basis: 30%, flex-basis: 100px 처럼 직접 값을 입력, 또 미디어 쿼리 안에서 이값을 조절, 이는 번거롭고 일관성 부족

## 작동 방식
flex-basis는 플렉스 컨테이너 메인축 방향으로 아이템이 차지할 초기 크기를 정함
- 가로정렬:  flex-row: flex-basis 아이템 너비를 의미한다.
- 세로 정렬: flex-col : felx-basis 아이템 높이 의미
실제로 늘어나거나 줄어들기 전에 적용되는 기준 크기가 된다.

## 사용법
스페이싱 스케일,퍼센트, 몇 가지 키워드를 이용한 flex-basis 클래스 제공
- 크기별 지정(basis-0,basis-px,basis-0.5,basis-1...basis-96)
	- basis-0: flex-basis: 0px; (시작 크기가0)
	- basis-16: flex-basis: 64px; (tailwind의 16단위 스케일에 따라 64px)
	- basis-\[10rem]: 직접 원하는 값(10rem)을 지정할 수 있다.
- 퍼센트 지정(basis-1/2, basis-full 등)
	- basis-1/2: flex-basis: 50%; (컨테이너 크기를 50%를 시작 크기로)
	- basis-1/3: flex-basis: 33.33333%;
	- basis-full: flex-basis: 100%;
- 키워드 지정:
	- basis-auto: flex-basis: auto; (기본값, 아이템의 내용물 크기에 따라 자동 결정)
```HTML
<div class="flex bg-gray-200 p-4">
	<div class="basis-1/4 bg-blue-300 p-2"> 나는 1/4크기로 시작</div>
	<div class="basis-1/2 bg-green-300 p-2"> 나는 1/2크기로 시작</div>
	<div class="basis-1/4 bg-red-300 p-2"> 나는 1/4크기로 시작</div>
</div>
```
> div는 각각 전체 flex 컨테이너 너비의 1/4, 1/2, 1/4을 기본크기로 가진다. 공간이 남거나 부족하면 flex-grow나 flex-shrink 설정에 따라 늘어나거나 줄어들게할수있겠죠

## 정리
늘어나거나 줄어들기 전 얼마만큼의 기본 크기를 가질지 아주 쉽게 설정해줄 수 있는기능이다. flexbox레이아웃을 만들 때 요소들의 기본 시작 크기를 정해준다.