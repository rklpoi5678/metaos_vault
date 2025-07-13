## 핵심
'나만의 특별한 도구'를 만들거나, '기존 도구를 나에게 맞춰 조금 변형' 하고 싶을때

## 필요할떄
- 아주 고유하고 복잡한 디자인 컴포넌트: 단순히 유틸리티 클래스를 조합하는 것만으로는 어렵거나, HTML 코드가 너무 길고 복잡  아주특별한 형태의 부품은 직접 만들어야 하는것과 같다.
- 재사용 가능한 고유 컴포넌트: 특정 디자인 패턴이 프로젝트 여러 곳에서 반복적으로 사용되는데, 매번 긴 유틸리티 클래스를 복사 붙여넣기 하는 게 비효율적일 때
- Tailwind에 없는 CSS 기능: 아주 특별한 CSS 속성이나 조합이 필요할때

## 나만의 스타일을 추가하는 주요 방법들
### **tailwind.config.js 파일 확장(Configuration)**
기본 팔레트(테마)에 나만의 색깔, 크기 , 폰트 등을 추가하거나 기존 것을 수정 가장 권장되는 방법이며, 가장 강력하다
```JS
// tailwind.config.js
module.exports = {
  theme: {
    extend: { // <-- 여기에 추가!
      colors: {
        'my-custom-blue': '#123456', // 'my-custom-blue'라는 새로운 색상 추가
        'accent': 'var(--color-accent)', // CSS 변수 사용도 가능
      },
      spacing: {
        '100': '25rem', // 'spacing-100'이라는 새로운 간격 추가
      },
    },
  },
  // ...
};
```

### **사용자 정의 CSS (@layer, @apply)**
 전통적인 CSS파일을 사용하되, 테일윈드의 기능을 활용하는것이다. 복잡한 컴포넌트 스타일을 만들거나, 외부 라이브러리의 스타일을 재정의할 때 유용하다.
1. CSS파일 만들기: 프로젝트에 src/styles.css 같은 CSS 파일을 만듭니다.
2. Tailwind지시문 포함: CSS 파일 맨 위에 Tailwind의 기본 스타일과 유틸리티 클래스를 포함시키는 지시문을 추가한다.

```CSS
/* src/styles.css */
@tailwind base; /* 테일윈드의 기본 스타일 */
@tailwind components; /* 테일윈드의 컴포넌트 유틸리티(선택 사항) */
@tailwind utilities; /* 테일윈드의 유틸리티 클래스 */
```
3. 나만의 CSS 작성: 이 파일 안에 일반 CSS규칙을 작성하되, @apply 지시어를 사용해서 테일윈드 유틸리티 클래스를 내 CSS 안에서 재사용가능하다.
```CSS
/* src/styles.css*/
@layer components { /* 'components'레이어에 추가하여 우선순위 관리 */
	.btn-primary {
		@apply bg-blue-500 text-white font-bold py-2 px-4 rounded; /* 테일윈드 유틸리티 조합 */
	}
	.card {
		@apply bg-white shaow-lg rounded-lg p-6;
	}
}

/* 아니면 직접 CSS 속성 추가 (추천하지 않는법, @apply을 최대한 활용) */
.my-custom-element {
	transform: rotate(15deg); /* 테일윈드에 없는 CSS 속성 직접 작성 */
}
```
-> 이제 HTML에서 class="btn-primary"처럼 내가 정의한 클래스를 사용할 수 있다. 이 클래스는 bg-blue-500 text-whilte ... 같은 테일윈드 유틸리티 클래스들의 묶음이 되는 것이다.
- 장점: HTML 코드를 더 깔끔하게 유지하면서도 테일윈드의 디자인 시스템을 활용할 수 있다. 복잡한 컴포넌트를 만들 때 효과적이다.
- @layer 지시문: base,components, utilities 같은 테일윈드 레이어 안에 내가 만든 CSS를 넣어서 CSS 우선순위 문제를 깔끔하게 관리 할 수 있도록 도와준다. 일반적으로 내가 만든 컴포넌트는 components레이어에 넣는것이 좋다.

### **인라인 스타일(arbitray values)**
아주 특별한 경웅만 사용하는 방법이다. tailwind.config.js에 추가하기도 애매하고, CSS파일에 따로 만들기 번거로울 때, HTMl 태그의 클래스 속성 안에 직접 CSS 속성 값을 넣어주는 방식이다.
-> 클래스 이름에 대괄호\[]를 사용해서 원하는 CSS속성 값을 직접 넣는다.
```HTML
<div class="top-[117px] left-[5%] bg-[#bada55] text-[2.5rem]">
	정말 특별한 위치와 색깔
</div>
```

> 정말 필요한 곳에서만 아주 유연하게 특별한 값을 사용할수있다.
> 이 값들은 테일윈드의 테마 시스템에 들어가지 않기 때문에, tailwind.config.js에서 값을 변경해도 자동 업데이트 되지 않는다. 그리고 코드를 읽기 어려워질 수 있어서 자주 사용하지 않는것이 좋다.

## 결론
1. tailwind.config.js 확장; 테일윈드의 나만의 색깔, 간격등을 추가하여 새로운 유틸리티 클래스를 만드는 가장 권장 되는 방법
2. 사용자 정의 CSS(@apply): 전통적인 CSS파일에 나만의 클래스를 만들고, 그 안에 테일윈드 유틸리티 클래스를 적용(@apply)하여 복잡한 컴포넌트를 만드는 방법
3. 인라인 스타일(\[]): 아주 특별하고 예외적인 경우에만, 클래스 이름에 직접 CSS 값을 넣어 사용하는 방법
개발자가 필요에 따라 유연하게 디자인 시스템을 확장하고 커스터마이징 할 수 있도록 도와준다.

