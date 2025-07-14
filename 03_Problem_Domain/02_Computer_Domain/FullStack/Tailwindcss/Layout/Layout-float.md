## 핵심
왼쪽에 붙여 아니면 오른쪽에 붙여 지시 -> 텍스트가 그 옆을 자연스럽게 감싸도록 만들어준다.

float는 까다로웠다. 해당 요소가 부모 요소를 벗어나거나, 다음에 오는 요소들이 이상하게 배치되는 문제가 자주 생겨 clear 같은 다른 속성으로 해결해야되었다.
요즘 flex,grid같은 더 유연하고 강력한 도구들이 있어 float는 잘 안쓴다.

## 플로팅 클래스
- float-left: 왼쪽으로 띄우고 , 다른 내용이 그 오른쪽으로 흐르게
- float-right: 위내용과 반대
- float-name: 플로팅 효과를 제거(기본값)

```HTML
<img src="사진.jpg" class="float-left mr-4">
<p>이 텍스트는 사진 옆으로 흐를 거예요.</p>
```
> img가 왼쪽, 텍스트가 그 옆을 감싸는형태

## 플로팅 해제하기: clear-left, clear-right, clear-both, clear-none
플로팅 요소 떄문에 다음 요소가 이상해질 때, clear클래스 사용 문제해결
- clear-left: 왼쪽 플로팅 요소 옆에 나타나는 것을 멈추고, 다음 줄로 내려가게 한다.
- clear-right: 반대
- clear-both: 양쪽 플로팅된 모든 요소 옆에 나타나는 것을 멈추고, 다음 줄로 내려가게한다.(가장 흔히 사용)
- clear-none: 클리어링 효과를 제거
```HTML
<img src="사진.jpg" class="float-left">
<p>이 텍스트는 사진 옆으로 흐를 거예요.</p>
<div class="clear-both"> 이 내용은 새로운 줄에서 시작해요.
</div>
```

## 요즘엔 float대신 뭘 쓰나요?
대부분 flex나 grid로 만들고 float는 필요한 경우 제한적으로 사용하고, 다음 요소에 영향을 주면 clear로 문제를 해결한다는 점이다.