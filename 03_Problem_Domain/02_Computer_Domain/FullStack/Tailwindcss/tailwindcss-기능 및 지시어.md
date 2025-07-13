## 핵심
함수와 디렉티브(Directives)가 무엇인지, 사용법을 알려주고
특별한 명령을 내리는 것과 미리 약속된 단축키라고 이해하면 좋다. 
복잡한 작업을 더 간단히, 그리고 더 똑똑하게 처리할 수 있도록 도와준다.

## tailwind 디렉티브: Tailwind의 핵심 주문
가장 먼저 알아야 할 것은 tailwind 디렉티브이다. 테일윈드에서 제공하는 모든 기본 스타일과 유틸리티 클래스를 우리 CSS파일에 '불러오는'주문이다.
- 왜 필요한지?: 테일윈드는 엄청 많은 유틸리티 클래스를 가지고 있지만, 이 클래스들은 우리가 일반 CSS 파일에 tailwind 디렉티브를 포함시켜야 비로소 작동하기때문
- 어떻게 사용가능한지?: 보통 프로젝트 메인 CSS 파일(src/main.css, src/globals.css)맨 위에 다음 세가지를 추가한다
```CSS
@tailwind base; /*tailwind의 기본 스타일 불러오기(브라우저 기본값 초기화등*/
@tailwind components; /*tailwind의 컴포넌트 관련 스타일 (선택사항)*/
@tailwind utilities; /*tailwind의 모든 유틸리티 클래스들을 불러온다.(가장 중요!*/
```
- @tailwind base: 브라우저마다 제각각인 기본 스타일 (버튼 모양, h1태그의 마진)을 tailwind가 정한 일관된 기준으로 초기화해주는 역할, 그림그리기 전 깨끗한 도화지를 준비하는것이다.
- @tailwind components: 일부 복잡한 컴포넌트 스타일(버튼이나 폼 요소 스타일)이 있다면 여기에 포함된다.(자주 사용은 안됨, tailwind 플러그인을 통해 추가된 컴포넌트 스타일이 여기에 포함될 수 있겠지요)
- @tailwind utilities: 핵심이다. bg-blue-500, text-xl,flex 같은 우리가 HTML에 직접 쓰는 수많은 유틸리티 클래스들이 여기에 포함된다. 이 부분이 없다면 Tailwind클래스들이 작동하지 않는다.

## @apply 디렉티브: 유틸리티 클래스들을 묶는 마법 단축키
여러 개의 Tailwind유틸리티 클래스들을 묶어서 나만의 새로운 CSS 클래스를 만들 때 사용한다.
- 전에도 보았다시피 bg-blue ... 처럼 여러 유틸리티 클래스가 하나의 디자인 패턴을 형성하고, 이 패턴을 여러 곳에서 반복적으로 사용해야 한다고 생각하자. HTML코드가 너무 길어지고 지저분해진다.
- 직접 만든 CSS 클래스 안에 @apply를 쓰고, 그 뒤에 묶고 싶은 Tailwind유틸리티 클래스들을 공백으로 구분해서 나열한다.
```CSS
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer components { /* @apply는 보통 @layer components 안에서 사용 */
	.btn-primary {
		@apply bg-blue-500 text-white font-bold py-2 px-4 rounded-lg;	
	}
	.card-itme {
		@apply bg-white shadow-md rounded-xl p-6 hover:shaodw-lg transition duration-300;
	}
}
```
> HTML에서 class="btn-primary" 또는 class="card-item" 만 사용하면된다. 최종 CSS만들때 이 클래스들을 @apply 뒤에 있는 유틸리티 클래스들로 다 풀어해쳐서 넣어준다.

### **장점**
- 재사용성: 복잡한 디자인 패턴을 한 번 정의해두고 여러 곳에서 class="btn-primary"처럼 간단하게 재사용 할 수 있다.
- 깔끔한 HTML: HTML코드가 휠씬 간결해지고 읽기 쉬워진다.
- Tailwind의 확장성: Tailwind의 디자인 시스템을 그대로 활용하면서도 나만의 컴포넌트 클래스를 만들 수 있다.

## @layer 디렉티브: CSS 규칙의 우선순위 관리 마법
@layer 디렉티브는 CSS 규칙들의 '우선순위'를 관리하는 데 사용된다. CSS에서는 나중에 정의된 규칙이나 더 구체적인 규칙이 우선권을 가지는데, @layer를 사용하면 이 복잡한 우선순위 문제를 테일윈드가 정한 규칙에 맞춰 깔끔하게 정리할 수 있다.

- 테일윈드 유틸리티 클래스는 기본적으로 매우 높은 우선순위를 가짐, 일반 CSS 규칙이 테일윈드 유틸리티 보다 우선하도록 만들고 싶거나, 반대로 테일윈드 유틸리티가 항상 우선하도록 만들때 필요하다.
- Tailwind는 세가지 기본레이어(base,components,utilities)를 가지고 있다.
```CSS
@tailwind base
@tailwind componets
@tailwind utilities

/* 내가만든 CSS를 레이어 안에 넣어준다. */
@layer base { /* base레이어: 브라우저 기본 스타일 초기화처럼 가장 기본적 스타일*/
	h1 {
		@apply text-3xl font-extrabold; /* h1 태그의 기본 스타일을 재정의*/
	}
}

@layer components { /* components레이어: @apply로 만든 컴포넌트 스타일 */
	.custom-btn {
		@apply bg-purple-500 text-white;
	}
}

@layer utilities { /* utilities레이어: @apply로 새로운 유틸리티 만드는 경우(드물다.) */
	.custom-text-red {
		@apply text-red-500 /* 새로운 유틸리티 클래스 정의 */
	}
}
```
> 우리가 정의한 CSS 규칙들이 Tailwind 기존 규칙들과 충돌하지 않고, 예측 가능한 순서와 우선순위로 적용되도록 보장해준다. 복잡한 CSS 우선순위 싸움에서 해방될 수 있다.

## theme() 함수: 설정 파일의 값을 CSS에서 사용하기
tailwind.config.js 파일에 정의한 '테마 값'들을 일반CSS에서 직접 가져와서 사용할수 있게 해주는 함수이다.
- tailwind.config.js에 colors.primary나 spacing.12처럼 나만의 디자인 토큰들을 정의했는데 그런데 src/main.css 파일에서 @apply를 쓰지않고 직접 CSS 속성을 정의하면서 이 값들을 쓰고 싶을 때가 있다.
- CSS 속성 값으로 theme('경로.경로.값')형태로 사용된다.
```CSS
@layer components {
	.btn-special {
		background-color: theme('colors.blue.500');
		/*config파일의 blue.500 색상 사용*/
		margin: theme('spacing.4');
		/*config파일의 spacing.4 값 사요*/
		font-family: theme('fontFamily.serif);
		/*config파일의 serif 폰트 사용*/
		box-shadow: 0 4px 6px -1px theme('colors.black / 0.1 );
		/*투명도도 적용 가능*/
	}
}
```
> 일반 CSS를 작성하면서도 Tailwind의 테마 시스템의 정의된 일관된 디자인 토큰들을 재사용할 수 있다. 숫자가 아닌 의미 있는 이름을 사용하니 가독성이 높아진다.

## 결론
함수와 디렉티브는 CSS 파일 안에서 Tailwind의 강력한 기능들을 불러오고, 활용하고, 확장하며, 관리할 수 있도록 해주는 주문이다. @tailwind로 기본 설정을 불러오고, @apply로 유틸리티를 묶어서 재사용하고, @layer로 우선순위를 정리하고, theme()로 설정 값을 가져와서 사용함으로써, Tailwind을 훨씬 더 유연하고 효율적으로 사용할 수 있게 된다.