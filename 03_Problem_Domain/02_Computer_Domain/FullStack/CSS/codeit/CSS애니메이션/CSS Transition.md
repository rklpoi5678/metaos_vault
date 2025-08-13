## 핵심
가장 강조하는 부분이다.
서서히 변하게 하는문법이 transition이다
`transtion: all 0.5s`

## 기본 속성
transition-property: width,height,color등만 지정하거나 모든 속성 값(all)을 지정할수있음
```CSS
transition-property: color, width;
```
transtion-duration: 속성 값이 변화가 진행되는 시간지정
초나 밀리초, 속성값이 여러개인 경우 쉼표로 구분
```CSS
transition-duration: 1s, 0.5s
```
transiton: transtion-duraiton, transtion-property을 짧게 줄여사용가능, 실제 사용할때 이방법이 훨씬 간편해서 더 자주사용된다.
```CSS
transition: color 1s, width 0.5s;
```

```CSS
.box {
  width: 100px;
  height: 100px;
  background-color: #32b9c1;
  transition: background-color 0.5s, width 0.5s, height 0.5s;
}

.box:hover {
  background-color: #e46e80;
  width: 200px;
  height: 200px;
}
호버시 백그라운드 컬러가 0.5초변화, 길이 0.5초변화, 높이 0.5초변화
```

## 부드럽게 적용하기
transition-timing-function: transition의 변화 속도를 지정할수있음 **베지에 곡선**을 사용해 속도 조절가능
![[Pasted image 20250814010739.png]]>Transtion 타이밍 함수에서는 4개의 점을 사용하는 3차 베지에 곡선이 사용됨

## 대표적인 타이밍 함수
ease: 기본값, 느리게 시작 점점 빨라지다 다시 느려지는 형태
linear: 처음부터 끝까지 같은 속도
ease-in: 느리게 -> 속도가 빨라짐
ease-out: 빠르게 -> 느리게
ease-in-out: 느리게 -> 빨라졌다 -> 다시 느려짐
cubic-bezier(p1,p2,p3,p4): 4점으로 베지에 타이밍 곡선을 커스텀가능

