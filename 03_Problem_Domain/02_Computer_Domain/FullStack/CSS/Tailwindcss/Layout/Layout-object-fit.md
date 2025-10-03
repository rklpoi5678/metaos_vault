## 핵심
사진이 액자 크게에 안 맞을 때 어떻게 채워 넣을까를 결정하는것이다. 꽉 채울것인지, 잘라서 채울 것인지, 아니면 원래 비율대로 작게 보여줄것인지

이미지,비디오를 div같은 공간에 넣을때 이미지/빋디오의 원래 비율과 공간의 비율이 다르면 문제가 발생한다.
- 공간을 벗어나거나, 너무 작아서 공간이 텅 비어보이거나, 찌그러지거나 등등
- 테일윈드는 CSS의 object-fit 속성을 사용해서, 이미지나 비디오가 할당된 공간에 어떻게 '맞춰질지'를 아주 쉽게 제어가능

## Tailwind의 object-fit 클래스 사용법
- `object-contain`: 사진을 원래 비율 그대로 유지, 액자안에 '모두 보이게'채워 넣는다. 액자 공간이 남을수도있다.
```HTML
<img class="w-48 h-48 object-contain" src="가로로_긴_사진.jpg">
```
- `object-cover`: 원래 비율 그대로 유지, 액자 공간을 '가득 채우도록' 늘려 넣는다. 사진의 일부가 액자 밖으로 잘려나갈수있다.
```HTML
<img class="w-48 h-48 object-cover" src="가로로_긴_사진.jpg">
```
- `object-fill`: 액자 공간에 '강제로 꽉 채워'넣는다. 사진의 원래 비율이 깨져서 찌그러질 수 있다.
```HTML
<img class="w-48 h-48 object-fill" src="정사각형_사진.jpg">
```

## object-position (사진 위치 조절)
cover나 contain으로 잘리거나 여백이 생길때 조절하고 싶다면 object-postion을 사용
- object-center: 사진의 가운데를 보여준다(기본값)
- object-top, object-bottom, object-left, object-right, object-left-top등 원하는 위치를 지정
```HTML
<img class="w-48 h-48 object-cover object-top" src="품경_사진.jpg">
```

## 정리
클래스를 이용해 이미지나 비디오가 할당된 공간에 어떤 방식으로 맞춰져서 보여질지 아주 쉽게 저어하는 기능이다.