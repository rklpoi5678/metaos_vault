## 핵심
물건이 상자 밖으로 넘칠 때 넘치는 부분을 어떻게 처리할까에 대한 내용이다.
숨길지, 스크롤해서 보게 할지 등을 결정

## 사용법
- overflow-auto: 넘치는 부분이 있다면 자동으로 스크롤바를 만들어보게해준다. 넘치지 않으면 스크롤바가 안생긴다.(가장 많이 사용)
```HTML
<div class="h-32 w-32 overflow-auto border">
	이것은 긴 텍스트입니다. 이 상자의 크기를 넘어서면 스크롤이 가능하게 됩니다. 
	더 많은 내용이 여기에 있습니다.
</div>
```
- overflow-hidden: 넘치는 부분을 그냥 잘라서 숨겨버린다. 숨겨진 내용은 볼수없게됨
```HTML
<div class="h-32 w-32 overfloew-hidden border">
	...
</div>
```
- overflow-clip: overflow-hidden과 비슷하게 자르지만, 스크롤바를 아예 불가능하게 만든다. (주로 브라우저 기본 스크롤 동작을 완전히 막을 때 사용)
- overflow-visible: 넘치는 부분이 그냥 상자 밖으로 튀어나오게 한다. 상자 밖으로 삐져나와도 그냥 둔다.
```HTML
<div class="h-32 w-32 overflow-visible border">
	...
</div>
```
- overflow-scroll: 넘치든 안 넘치든 항상 스크롤바를 만들어서 보여줌
```HTML
<div class="h-32 w-32 overflow-scroll border">
	짧은 텍스트
</div>
```
- overflow-x-auto, overflow-y-hidden등: 가로 또는 세로 방향으로만 오버플로우를 따로 처리할수도 있다.

## 정리
내용물이 넘칠때 어떻게 보여줄지 (숨길지, 스크롤할지, 튀어나오게 할지) 쉽게 제ㅐ어하는 기능이다.

