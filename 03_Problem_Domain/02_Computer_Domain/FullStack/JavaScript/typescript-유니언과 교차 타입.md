## 핵심
기본적인 타입을 가지고 더 복잡하고 유용한 타입을 만드는 '조합 도구'라고 생각하면 이해하기 쉽다.

## 유니언 타입 (Union Types): 이것 아니면 저것이다!
여러 타입 중 하나가 될 수 있는 값을 의미한다. "이 상자 안에는 사과 아니면 배가 들어있을 거야"라고 말하는 것과 같다. 둘다 가능하다.
- 표현법: 타입들 사이에 파이프 기호,
- 왜 쓸까?: any타입을 썻는데 any는 워낙 자유로워 실수를 잡아주지 못한다. 유니온 타입을 쓰면 이 나열된 타입들 중에서만 사용이 가능하다고 명확히  알려줄수있어 프로그램이 안전해진다.`function printId(id: number | string)` 이 함수는 id가 숫자이거나 문자열일 수 있다는 걸 명확히 한다.
- 주의점: 유니언에 있는 모든 타입이 공통으로 가지고 있는 속상만 사용할수있다. `string에 length속성이 있지만 number에는 없다. 그래서 number | string 타입의 변수는 바로 .length를 쓸수없다. 이럴때는 타입 좁히기 라는 것을 사용하여 현재 변수의 실제 타입을 확인해야한다.`

## 유니언 구별하기 (Discrimination Unions): 어떤 상태인지 정확히 알기
유니언을 이루는 각 타입들이 공통적으로 가지고 있는 특정 필드(속성)을 사용해서 현재 상태를 판별하는 방식이다.
- 리터럴 타입(특정 문자열이나 숫자 값)을 가지는 하나의 필드를 공유해야 한다.

```ts
interface LoadingState {
    state: "loading"; // 리터럴 타입 "loading"
}
interface SuccessState {
    state: "success"; // 리터럴 타입 "success"
    data: any;
}
interface ErrorState {
    state: "error";   // 리터럴 타입 "error"
    message: string;
}

type NetworkState = LoadingState | SuccessState | ErrorState;
```
state는 필드가 각 타입마다 다른 리터럴값을 가지고있는데 NetworkState 타입의 변수를 switch문으로 검사하면서 state필드의 값을 확인하면, 현재 변수가 LoadingState인지 다른 스테이트인지 타입스크립트가 정확히 알게된다.

## 교차 타입(Intersection Types) 이것도 되고 저것도 되는 모든 기능 합치기
- 표현법: 타입들 사이에 `&(앰퍼샌드)` 기호를 사용한다. `Persion & Serializable & Loggable`은 Person이면서 동시에 Serializable이고 Loggable인 객체라는 뜻이다.
- 왜쓸까?: 여러 타입의 기능을 한 번에 묶어서 새로운 타입을 만들때 사용한다. 여러 블록을 합쳐서 더 크고 복잡한 구조를 만드는것이다.
- `이미지 목록을 불러오는 응답 타입이 ArtworksData와 ErrorHandling` 두가지의 인터페이스의 속성을 모두 가져야 한다면, `type ArtworksResponse = ArtworksData & ErrorHandling`처럼 만들수있다. 이렇게 하면 ArtworksResponse는 ArtworksData의 속성과 ErrorHandling의 속성을 모두 가지게 된다.

## 교차를 통한 믹스인 (Mixins via Intersections) 기능을 섞어서 새 도구 만들기
믹스인은 특정 기능을 여러 클래스에 재사용하고 싶을 때 사용하는 패턴이다. 타입스크립트에서는 교차 타입을 활용해서 믹스인 패턴을 구현할수있다.
- 속성과 메서드를 한데 섞어서 새로운 클래스를 만든다.
- `Person이라는 기본 클래스가 있는데, 여기에 Loggable이라는 인터페이스의 기능을 추가하고 싶다고 한다면, 교차 타입을 이용해서 extend같은 유틸리티 함수를 만들면, Person클래스의 Loggable의 기능이 합쳐진 새로운 클래스를 만들 수 있다.`
- 이는 기본 망치에 '나사 돌리는' 기능을 추가해서 만능 망치를 만드는 것과 비슷하다. 기존 망치에 나사돌리는 기능을 교차해서 더 많은 기능을 가진 도구를 만드는 것이다.
