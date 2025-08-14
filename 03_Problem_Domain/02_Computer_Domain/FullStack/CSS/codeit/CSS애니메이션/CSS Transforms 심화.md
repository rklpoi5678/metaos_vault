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

