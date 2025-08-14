## 3D Transforms

rotateX(angle)
요소를 x축 기준으로 주어진 각도만큼 회전합니다.
![[Pasted image 20250814094928.png]]
rotateY(angle)
요소를 y축만큼 회전시킵니다.
![[Pasted image 20250814094956.png]]
rotateZ(angle)
요소를 z축을기준으로 주어진 각도만큼 회전
![[Pasted image 20250814100000.png]]

traslateZ(z)
요소를 z축으로 이동

translate3d(x,y,z), rotate3d(x,y,z,angle), scale3d(x,y,z)
x,y,z: 3축을 기준으로 요소를 한 번에 이동,회전,확대 및 축소를 할수있게 해줍니다.
rotate3d()함수에서 x,y,z는 회전축 방향을 의미한다. 일반적으로 1이나 -1 사이 값을 사용하고 음수는 축의 방향을 반대 방향으로 돌리게 된다.

persepective속성과 perspective(value)함수
깊이감과 거리감을 만들어서 요소를 진짜 입체적으로 보이게 할수있다.

## perspective 속성
요소의 부모에 적용, 부모 요소에 적용된 perspective는 자식 요소에 영향을 미쳐 깊이감을 더해준다.

perspective(value) 함수
변형하려는 요소에 직접 사용된다.
**값이 크면** 요소가 더 멀리 떨어진 것 처럼 보여 **요소가 덜 왜곡되며 더 평평**해 보이고, **값이 작으면** 요소가 가까이 있는 것처럼 보여 **요소가 더 왜곡되고 극적인 효과가 나게됨**


## transform-origin
기본 이동,회전등 모든 요소의 변형 중심 기준 이 함수를 사용하면 그 기준점을 변경할수있다.
```CSS
transform-origin: x y z;
```
>px,% 단위로 설정하거나, left,center,right(x축),top,center,bottom(y축)로 설정할수있다.
>transform-origin: left top; 은 왼쪽 위를 기준점으로 설정한다는 말이다.
추가로 x세로선 왼쪽 좌우를 움직인다는 느낌이고 y는 가로선을 아래 위로 움직인다는 느낌이다.

## transform과 transition 함께사용
```CSS
.box {
	width:100px;
	height: 100px;
	margin: 40px auto;
	background-color: rgb(255, 68, 99);
	transition: tran
}
```