## 핵심
일반적인 CSS 문제점인 background-color: #FF0000;(빨간색) 또는 color: rgb(0,0,255);(파란색)처럼 색상 코드르 직접입력해야 되었다.
이러한 방식은 외우기어렵고, 디자이너가 정해준 특정 색상 시스템을 모든 개발자가 일관되게 사용하기 어려웠다.

테일윈드는 미리정의된 잘 구성된 '색상 빨레트'를 제공한다. 다양한 농도(톤) 100부터 900까지 100단위로 숫자로 구분되어 있다.
- bg-blue-500: 배경색을 파란색 계열의 500번 톤으로 해줘
- text-red-600: 글자색을 빨간색 계열의 600번 톤으로 해줘
- border-gray-300: 테두리 색깔을 회색 계열의 300번 톤으로 해줘

## 테일윈드의 기본 색상 팔레트 (미리 준비된 물감들)
- 회색 계열: gray,zinc,neutral,stone,slate 등
	- text-gray-500(중간 회색)
	- bg-slate-900 (아주 어두운 청회색)
- 빨강: red
	- text-red-500 (표준 빨강색)
- 주황: orange
- 노랑: amber, yellow
- 초록: lime,green,emerald,teal
- 파랑: blue, indigo, purple
- 자주: fuchsia,pink,rose
- 흰색/검은색: white, black(이들은 톤이 없다. 그냥 text-white, bg-blackc처럼 사용)
- 투명: trasparent(투명한 색상)
	- bg-transparent
이 외에도 다양한 색상이 기본적으로 제공되며, 대부분의 디자인 요구사항을 충족시킬수있다.

## 색상 유틸리티 클래스 사용법 (팔래트에서 색상 꺼내 쓰기)
매우 직관적이다ㅏ. \[속성]-\[색상이름]-\[색상 톤] 형식의 클래스를 HTML요소에 추가하기만 하면 된다.
- 글자색(text-\[색상]):
```HTML
<p class="text-blue-500">파란색 글자</p>
<span class="text-red-600">빨간색 글자</span>
```
- 배경색(bg-\[색상]):
```HTML
<div class="bg-gray-200">연한 회색 배경</div>
<button class="bg-emerald-700">초록색 버튼</button>
```
- 테두리 색상(border-\[색상]):
```HTML
<input type="text" class="border border-indigo-400">
```
- 다른 속성들도 가능하다: 테두리 분할 색상(divide-\[색상]), 그림자 색상(shadow-\[색상]), 강조 색상(accent-\[색상]), 캐럿 색상(caret-\[색상]), 채우기 색상(filll-\[색상]), 스트로크 색상(stroke-\[색상]), 링 색상(ring-\[색상])등등 대부분의 색상 관련 CSS 속성에 `[속성]-[색상 이름]-[색상 톤]` 패턴으로 적용할 수 있다.

## 기본 색상 외에 나만의 색상 추가하기(나만의 물감 만들기)
만약 우리 프로젝트만의 특별한 브랜드 색상이 있다면 어떻게 해야하는가?
- tailwind.config.js 파일에서 theme.extend.colors 안에 나만의 색상을 추가할수있다.
```JavaScript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        'brand-primary': '#1A73E8', // 우리 브랜드의 메인 파란색
        'brand-secondary': '#FF6F00', // 우리 브랜드의 포인트 주황색
      }
    }
  }
}
```
이렇게 추가하면 이제 text-brand-primary, bg-brand-secondary 같은 유틸리티 크래스를 사용할수 있다
- 전체 색상 팔레트 덮어쓰기: 당연히 extend없이 theme.colors에 직접 정의하면 된다.(하지만 보통은 extend를 사용해서 기본 색상을 유지하는 것이 편리하다.)


## 불투명도 조절하기(물감의 농도 조절)
색상의 투명도를 조절하고 싶을 때는 /(슬래시) 뒤에 퍼센트 값을 붙인다.
- bg-blue-500/50: 파란색 500번 톤에 투명도를 50% 적용
- text-black/75: 검은색에 투명도를 75% 적용

## 결론
미리 정의된, 체계적인 색상 팔레트와 간결한 유틸리티 클래스를 제공해서 웹 디자인에서 색상을 일관성있고 효율적으로 관리할 수 있게 해준다. 복잡한 색상 코드를 외우거나 직접 입력할 필요 없이, 이름만으로 원하는 색상과 톤을 바로 적용할 수 있는 강력하고 편리한 도구이다.