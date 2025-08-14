## 핵심
주변 요소들의 영향을 미치지 않고 특정 요소의 크기,형태,위치 등을 변경할 수 있다.
transfrom: transform-function;를 적어서 사용할수 있는데, transform-function은 특별한 CSS  함수가 들어가는 부분

주의할점으로 여기서 쓰이는 y축은 양수일경우 아래로 움직인다.

## Transform 함수 종류
`translate(x, y), translateX(x), translateY(y)`
![[Pasted image 20250814093701.png]]
>오른쪽으로 20px, 아래로 10px이동시킨다. 

scale(x,y), scaleX(x), scaleY(y)
요소를 주어진 크기만큼 확대하거나 축소한다.
![[Pasted image 20250814093831.png]]
>scale(2, 0.5)는 요소를 가로로 2배, 세로로 0.5배 크기로 만든다.(배수)

skew(x-angle,y-angle), skewX(x-angle), skewY(y-angle)(기울임)
![[Pasted image 20250814094123.png]]
> 주어진 각도만큼 x축과 y으로 기울인다.

## rotate(angle)
요소를 주어진 각도만큼 회전시킨다. rotate(30deg)는 요소를 30도 회전시킨다. 각도 단위로는 deg, rad, grad, turn이 사용된다.
![[Pasted image 20250814094301.png]]

## 같이 사용
```CSS
transform: translate(20px) scale(0.5) rotate(30deg);
```
