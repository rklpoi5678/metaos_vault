## 핵심
가로와 세로의 '황금 비율'을 딱 맞춰서 빈 공간 없이 예쁘게 보이게 하는것과 같다.

## 화면비율
이미지,비디오 또는 지도 이런 요소들은 고유한 가로-세로 비율을 가지고있다ㅏ.
- 만약 너비지정 높이는 지정하지 않을시, 브라우저가 기본값으로 높이를 계산 -> 이미지가 비율에 맞지 않게 늘어나거나 찌그러져 보일 수 있고, 로딩될때까지 공간이 제대로 확보가 안되어 웹 페이지의 레이아웃이 뚝뚝 끊기는(점프하는)현상이 발생할수있다.
- 특히 반응형 디자인에서는 너비가 유동적으로 변하므로 높이도 그에 맞춰 비율을 유지하는 것이 중요하다.
```HTML
<img src="my-image.jpg" class="w-full">
```
CSS로 직접 비율을 맞추려면  padding-top을 이용하는 트릭(padding-top: N%로 높이 확보)을 사용하거나, JS로 계산하는 등 번거로운 방법이 필요하였다.

-> 이 문제를 Tailwind는 aspect-ration유틸리티 클래스로 아주 간단하게 해결한다.
-> aspect-\[가로]/\[세로] 형식
넣어주면, 요소가 어떤 머비를 가지든 항상 정해진 가로-세로 비율을 유지하도록 만들어준다.
> 이사진을 항상 16:9 비율로 보여줘 라고 정확히 지시하는 것과 같다.
```HTML
<div class="aspect-w-16 aspect-h-9">
	<iframe src="..."></iframe>
</div>

<div class="aspect-video">
	<iframe src="..."></iframe>
</div>

<div class="aspect-[16/9]">
	<img src="my-image.jpg" alt="Description">
</div>
```
> 이제 이 div는 너비가 변해도 항상 16:9 또는 4:3 비율의 높이를 자동으로 가지게 된다.

## 화면 비율 사용법(황금 비율 맞추는 법)
### **숫자기반 비율(aspect-\[가로]/\[세로])**
가장 일반적,유연
- aspect-\[16/9]: 가장 흔한 비디오 비율
- ..4/3 전통적인 TV나 카메라 비율
- ... 1/1 정사각형 유지
- ... 21/9 울트라 와이드 모니터 비율을 유지
```HTML
<div class="aspect-[16/9]">
	<img src="video-placeholder.jpg" class="w-full h-full object-cover" alt="Video">
</div>
```
> 이 클래스를 가진 요소는 너비가 아무리 변해도 항상 16:9비율의 높이를 자동으로 가집니다. 안에 있는 이미지나 비디오는 w-full h-full boject-cover 같은 클래스로 부모에 꽉 차게 만들 수있다.

### **미리 정의된 키워드 비율 (Semantic Classes)**
자주 사용되는 몇 가지 비율에 대해 더 간편한 키워드 클래스도 제공
- aspect-auto: 기본값, 요소가 원래 가지고 있는 비율 그대로 유지
- aspect-square: aspect-\[1/1] 동일. 정사각형
- aspect-video: aspect-\[16/9]와 동일. 비디오 비율
```HTML
<div class="aspect-video"><iframe src="https://www.youtube.com/embed/,,." frameborder="0" allowfullscreen></iframe></div>
```

### **반응형 디자인과 결합(다양한 화면에 맞게 비율 변경)**
반응형디자인 접두어(md:,lg:)와 함께 사용하여 화면 크기에 따라 비율을 다르게 설정할수있다.
```HTML
<div class='aspect-[4/3] md:aspect-video lg:aspect-[21/9]'>
	<img src="my-hero-image.jpg" class="w-full h-full object-cover" alt="Hero Image">
</div>
```
> S,M,L사이즈에 따라 핏이 조금씩 달라지는것, 화면 크기에 따라 가장 적절한 비율을 선택하도록 지시하는것

## 유용성
- 일관된 레이아웃: 사용자 경험향상, 로딩전 정확한 공간을 미리확보하여 웹 페이지 레이아웃이 '점프'하는 것을 방지
- 반응형 완벽 지원: 요소의 비율이 깨지지 않고 유지됨
- 간결한 코드: 복잡한 CSS 핵이나 JavaScript없이 HTML클래스만으로 쉽게 비율을 제어할 수 있다.

## 결론
aspect유틸리티 가로/세로 -> 어떤 화면 너비에서든 항상 지정된 가로-세로 비율을 유지하도록 만들어주는 매우 유용한 기능이다.