## 핵심
웹을 어둡게, 글씨를 발게 바꿔서 눈의 피로를 줄여주고 배터리 소모를 아껴주는 기능이다.

일반적으로 다크 모드를 만들려면 CSS에서 :root셀렉터나 특정 클래스(.dark-mode)를 정의하고, 밝은 모드일 떄와 어두운 모드일 때의 모든 색상 변수를 일일이 설정해야 했다. HTML에도 다크모드 클래스를 추가하거나 제거하는 JavaScript코드는 덤이고, 이 과정이 복잡하고, 많은 CSS 코드를 관리해야 하는 번거로움이 있었다.

테일윈드는 유틸리티 클래스 방식으로 매우 간결하게 해결해 준다. dark: 라는 접두어를 붙여주기만 하면, 해당 요소가 다크 모드일 때 적용될 스타일을 아주 쉽게 지정할 수 있다.
```HTML
<dv class="bg-white dark:bg-gray-800 text-black dark:text-white p-6 rounded">이 글자는 낮엔 검정, 밤엔 하양이다.</div>
```

- bg-wihte text-black: 기본적으로는 배경색은 흰색, 글자색은 검정색(밝은모드)
- dark:bg-gray-800: 다크 모드일 때는 배경색을 어두운 회색(gray-800)으로 바꿔준다.
- dark:text-white: 다크 모드일 때는 글자색을 흰색으로 바꿔준다.
이렇게 dark: 접두어만 붙여주면, 해당 스타일은 다크 모드일 때만 적용된다.

## 다크 모드 활성화 방식 선택하기(기준 설정)
이 방식은 tailwind.config.js파일에서 설정할 수 있다.
### **media방식(기본값, 사용자 시스템 설정 따라가기)**
- 설정 darkMode: 'media'(기본값이라 따로 설정하지는 않아도됨)
- 작동은?: **운영체제(Windows, macOS, Android, iOS등) 설정**을 따라간다. 사용자가 컴퓨터나 스마트폰을 '다크 모드'로 설정해 두었다면, 웹사이트도 자동으로 다크 모드로 보여진다.
- 장점: 자신의 기기 설정에 맞춰 편리하게 다크 모드를 경험할 수 있다. 대부분의 웹사이트가 이방식을 차용함
### **class 방식(사용자에게 직접 선택권 주기)**
- 설정 darkMode: 'class'
- 작동은? 웹사이트 \<html>태그에 dark라는 CSS클래스가 있는지 없는지에 따라 다크 모드가 작용된다.
	- \<html>태그에 \<html class="'dark">가 있다면 다크 모드 스타일이
	- \<html class="">(또는 dark클래스가 없다면) 밝은 모드 스타일이 적용됨
- 장점: 웹내 '다크 모드 켜기/끄기'버튼을 만들어서 사용자가 직접 다크 모드를 제어할 수 있게 할때 유용하다. 이 버튼을 누르면 JS로 \<html> 태그의 dark클래스를 추가하거나 제거하는 방식으로 동작한다.
<html lang="ko">
<body>
  <div class="bg-white dark:bg-gray-800">...</div>
  <button onclick="document.documentElement.classList.add('dark')">다크 모드 켜기</button>
</body>
</html>

<html lang="ko" class="dark">
<body>
  <div class="bg-white dark:bg-gray-800">...</div>
  <button onclick="document.documentElement.classList.remove('dark')">다크 모드 끄기</button>
</body>
</html>

## 결론
**사용자 설정이나 직접적인 제어에 따라 밝은 모드와 어두운 모드를 유연하게 전환**  할 수 있도록 해준다. CSS나 JS없이 HTML안에서