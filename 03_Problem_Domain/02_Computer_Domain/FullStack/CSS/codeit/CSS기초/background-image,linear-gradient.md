## 핵심
백그라운드로 이미지 삽입가능
그라디언트 효과를 줄수있으며
linear-gradient + background-image 조합으로 사용이가능하다.

## background-image 속성
```CSS
background-image: url('flowers.png');

/* 배경 이미지는 여러개 넣을수있음 */
background-image:
  url('a.png'), /* 제일 위에 보이는 이미지 */
  url('b.png'), /* a.png아래 깔림*/
  url('c.png'); /* ... */

```
```CSS
background-position: top; /* 위 */
background-position: right; /* 오른쪽 */
background-position: bottom; /* 아래 */
background-position: left; /* 왼쪽 */
background-position: left top; /* 왼쪽 위 (지정하지 않았을 때 기본값) */
background-position: center;

```
```CSS
background-repeat: repeat; /* 반복하기 (지정하지 않았을 때 기본값) */
background-repeat: no-repeat; /* 반복 안 함 */

```
```CSS
background-size: cover; /* 비율 유지하면서 꽉 차게. 이미지 잘릴 수 있음 */
background-size: contain; /* 비율 유지하면서 최대한 크게. 이미지 잘리지 않음 */
background-size: 40px 30px; /* 가로 40px 세로 30px */

```
background-image: url("");
background-repeat: no-repeat;
background-position: center;
background-size: cover;

## linear-gradient 속성
```CSS
/* 시작 색상과 종료 색상으로 사용가능*/
 background-image: linear-gradient(#000000, #ffffff);

/* 기본각도는 180도(위에서 아래로 내려오는 방향) 이각도를 수정할려면 맨앞에 deg단위를 써서 조절가능하다. */
background-image:
  linear-gradient(45deg, rgba(0, 0, 0, 0.8), rgba(0, 0, 0, 0.2));

```
예시: linear-gradient(90deg, rgba(0,0,0,0),40%, rgba(0,0,0,0.5))

혼합해서 사용시
linear-gradient(\~\~\~), url("");

