## 핵심
공간을 어떻게 '유연하게' 채울지 결정하는것

## 해결책
- CSS는 flex-grow,flex-shrink,flex-basis 3가지 속성을 조합해 사용 flex: 1 1 0% 처럼 복잡하게 써야했는데, 이건 외우기 어렵고, 매번 코드를 작성하기 번거로웠다.
- 세가지 속성을 조합한 flex유틸리티 클래스와 각각을 개별적으로 제어하는 클래스를 제공해

## 사용법
flex-1: 가장 많이 쓰는 옵션: 이건 flex: 1 1 0% 과 같다. 남은 공간이 있으면 똑같이 늘어나서 다 차지한다. 그리고 최소한 0px크기까지 줄어들수있다라고 얘기하는것과 같다.(자리를 공평하게 준다.)
```HTML
<div class="flex w-full">
	<div class="flex-1 bg-blue-200 p-4">Item 1</div>
	<div class="flex-1 bg-green-200 p-4">Item 2</div>
	<div class="flex-1 bg-red-200 p-4">Item 3</div>
</div>
```
flex-auto: 이건 flex: 1 1 auto와 같다. 남는 공간이 있다면 늘어나고 필요시 원래 내용물 크기까지 줄어들 수 있다. flex-1과 비슷한데 flex-basis가 auto라서 아이템의 초기 콘텐츠 크기를 존중한다.
```HTML
<div class="flex w-full">
    <div class="flex-auto bg-blue-200 p-4">짧은 내용</div>
    <div class="flex-auto bg-green-200 p-4">조금 더 긴 내용입니다.</div>
</div>
```
![[Pasted image 20250714152934.png]]
flex-inital: flex: 0 1 auto와 같다 늘어나지 않는데 필요시 내 원래 내용물 크기까지는 줄어들수있다고 말하는것과 같다.
![[Pasted image 20250714153013.png]]
flex-none: flex: 0 0 auto; 와 같다 절대 늘어나지도, 줄어들지도 않을것이다. 내 원래 크기를 그대로 유지하겠다. 즉, 고정된 크기의 아이템에 사용한다.

### **개별 속성 제어(선택 사항)**
flex-grow(늘어나는 정도), flex-shrink(줄어드는 정도), flex-basis(시작크기)를 따로따로 제어하는 클래스도 사용할 수 있다.
- grow: flex-grow: 1; (남은 공간을 차지)
- grow-0: flex-grow: 0; (늘어나지 않음)
- shrink: flex-shrink: 1; (공간 부족 시 줄어듦)
- shrink-0: flex-shrink: 0; (줄어들지 않음)
- basis-1/2, basis-32, basis-auto 등: 아이템의 시작 크기 지정

## 정리
남은 공간을 어떻게 채우고, 공간이 부족할 때 어떻게 크기를 조절할지 아주 쉽고 직관적으로 제어하는 핵심기능이다.
어떤 화면크기에서도 유연하고 반응적인 웹 레이아웃을 만들수있다.