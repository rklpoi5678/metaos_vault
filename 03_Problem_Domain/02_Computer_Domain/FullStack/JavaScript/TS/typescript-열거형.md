## 핵심
그냥 숫자로 `0,1,2` 또는 문자열로 `Red,Green,Blue`라고 직접 코드에 쓰면 나중에 헷갈리거나 오타가 났을 때 찾기 힘들다. 0이뭔지 1이 뭔지 한눈에 알기 어렵고, Rred라고 오타를 내도 컴퓨터는 그냥 문자열로 인식

- 해결책: Enum 은 이런 문제를 해결하기 위해 관련된 값들을 한데 모아 '이름'을 붙여준다. 이제부터 0은 요일.월요일이야 1은 요일.화요일이야 라고 약속하고, 그 이름으로만 사용하도록 강제하는겁니다. 코드 가독성과 인적 문제, 오타로 인한 버그를 타입스크립트가 미리 잡아줄 수있다.

```ts
enum Direction {
	Up,      //0
	Down,    //1
	Left,    //2
	Right    //3
}

let userDirection: Direction = Direction.Up; // 이제 0이 아니라 UP이라고 명확하게 쓸 수 있어요
```

## 숫자형 Enum (Numerice Enums): 기본 동작 방식
가장 흔하게 사용됩니다.
- 자동으로 숫자부여: Enum멤버의 값을 따로 지정해주지 않으면, 첫번째 멤버부터 0부터 순서대로 숫자가 자동으로 부여가된다. UP 0, Down 1, Left는 2, Right는 3이 되는격이다.
- 시작 숫자 변경: 첫 번째 멤버에만 숫자를 지정해주면, 그 다음 멤버부터는 1씩 증가하면서 숫자가 부여된다.
```ts
enum UserResponse {
	No = 1, //No는 1
	Yes,    //Yes는 자동으로 2가 된다.
}
```
- 수동으로 값 지정: 모든 멤버에 직접 숫자를 지정해줄 수도 있다.
```ts
enum Status {
	Pending = 100,
	Approved = 200,
	Rejected = 300
}
```
- 양방향 매칭: 숫자형 열거형은 특징이 열거형 멤버 이름으로 숫자를 알 수 있을 뿐만 아니라, 숫자로 멤버 이름을 다시 알아낼 수있다.
- Direction.Up은 0.
- Direction\[0]은 "Up".
- 이건 Enum이 컴파일된 자바스크립트 코드에서 객체 형태로 만들어지기 때문인데, 너무 깊게 생각하지 않아도 괜찮다. 그냥 양쪽으로 통하는 길이 있다는 느낌이다.

## 문자열 Enum (String Enums): 더 명확하게!
숫자대신 문자열을 값으로 가지는 Enum
- 값명시 필수: 숫자형과 다르게 문자열은 모든 멤버에 값을 직접 지정한다. 타입스크립트가 자동으로 문자열을 부여해주지 않는다.
- 장점: 코드 가독성이 휠씬 좋다. 코드만 봐도 어떤 의미인지 알수있으니
- 단점: 숫자형처럼 '양방향 매핑'이 안된다. get으로 httpmethod.get을 알아낼 수는 없다. 오직 httpmethod.get 으로 get만 알수있다.

## 이종 Enum(heterogeneous Enums): 섞어 쓰기 (잘 사용은 안함)
숫자형과 문자열형 멤버를 섞어서 사용하는 열거형
```ts
enum Mixed {
	No = 0,
	Yes = "YES"
}
```
! 거의 사용되지 않고, 혼란을 줄 수 있어서 추천하지 않는 방식이다.

## 상수 Enun (Const Enums): 더 가볍고 빠르게!
enum키워드 앞에 const를 붙여서 만드는 Enum
- 컴파일된 자바스크립트 코드에 Enum 객체 자체가 남는 것을 원치않을때 사용한다. enum객체가 만들어지지 않으니 코드 크기가 줄어들고 , 실행 속도가 빨라질 수 있다.
- 동작방식: 타입스크립트 컴파일러가 상수 Enum의 값을 코드에 직접 박아 넣는다 (인라인)

```ts
const enum Colors {
	Red,
	Green,
	Blue
}

let myColor: Colors = Colors.Red
// 이 코드는 컴파일되면 'let myColor = 0;' 으로 바뀝니다. 
// Colors라는 Enum 객체는 JavaScript 코드에 남지 않아요.
```

```ts
// E.X는 상수이다.
	enum E { X }
```
```ts
// 'E1' 과 'E2' 의 모든 열거형 멤버는 상수이다.
enum E1 { X, Y, Z }
enum E2 {
	A = 1, B, C
}
```
- 양방향 매핑이 불가능하고, 런타임에 Enum 객체를 직접 참고할 수 없다. 즉, Colors.Red는 가능한데 Colors\[0]은 불가능하다.

## 주변 Enum(Ambient Enums): 이미 존재하는 Enum 사용하기
다른 자바스크립트 코드나 라이브러리에 이미 Enum과 비슷한 개념이 정의되어 있을 때, TytpeScript에서 그 Enum을 `declare` 키워드를 사용해 '선언'만 해주는 것이다. 실제 구현은 없고, 타입 정보만 타입스크립트에 알려주는 것이다.

```ts
declare enum ExternalLibEnum {
	Value1,
	Value2,	
}
```
주로 외부 라이브러리를 사용할 때 그 라이브러리에 있는 Enum을 타입스크립트가 인식하도록 타입 정의 파일을 만들 때 사용

Enum은 코드를 더 안전하고 읽기 쉽게 만들어주는 좋은 기능이다. 특히 숫자형Enum과 문자열 Enum은 실무에서 자주 사용되니 꼭 기억해두자.

## 역 매핑 (Reverse mappings)
```ts
enum Enum {
	A
}
let a = Enum.A;
let nameOfA = Enum[a]; // "A"
```
문자열 열거형은 역 매핑을 생성하지 않는다는것을 명심

