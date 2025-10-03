## 핵심
Layout-object-fit 목차 참고

css의 object-postion속성을 사용해 어느위치를 기준으로 배치될지를 아주 쉽게 제어

## 사용법
- object-center(기본값)
- object-top(아래쪽이 잘릴 수 있음)
- object-bottom
- object-left
- object-right
- object-left-top,..right-top,...left-bottom,...right-bottom: (코너 모서리)부분을 기준으로 맞춘다.
- `object-[x-위치],object-[y-위치]` 또는 `object-[x-위치_y-위치]`: 직접 퍼센트나 픽셀 값으로 위치를 지정할 수 있다
	- `object-[25%]`:(가로25%지점)
	- `object-[0%_100%`:(왼쪽 아래)
