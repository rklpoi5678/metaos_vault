## 핵심

## React에서 컴포넌트란?

React에서 **컴포넌트(Component)** 는 UI를 구성하는 **독립적이고 재사용 가능한 코드 블록**입니다. 각각의 컴포넌트는 JSX를 반환합니다.

이러한 기능으로 재사용이 가능하며 , 상태 관리와  프롭스 전달이 용이해집니다.
##  함수형 컴포넌트
함수형 컴포넌트는 함수기반으로 useState, useEffect, HooK을 사용하며 상태의 생명주기를 useEffect등의 훅으로 대체한다. 간결하고 직관적이다. 현재는 리액트에서는 함수형 컴포넌트를 사용합니다.
##  클래스 컴포넌트
클래스 컴포넌트는 클래스기반으로 일반 클래스처럼 this.state, this.setState를 사용하였다. 생명주기는  componentDidMount, componentDidUpdate 등을사용한다. 상대적으로 복잡하고 장황하다.


##  useMemo & useCallback 설명

### `useMemo`

`useMemo`는 **값을 메모이제이션**(값을 넣어놔서)하여 불필요한 계산을 방지합니다.

```js
const expensiveValue = useMemo(() => computeHeavyTask(a, b), [a, b]);
```

- **언제 사용하나?**
    
    - 계산 비용이 큰 함수 결과를 저장하고 싶을 때
    - 렌더링마다 동일한 계산을 반복하는 경우
- **주의점**
    
    - 의존성 배열이 정확하지 않으면 잘못된 값이 캐싱됨
    - 너무 자주 사용하면 코드 가독성과 유지보수에 악영향

### 🔹 `useCallback`

`useCallback`은 **함수를 메모이제이션**하여 불필요한 함수 재생성을 방지합니다.

```js
const handleClick = useCallback(() => doSomething(id), [id]);
```

 **언제 사용하나?**
 
    - 자식 컴포넌트에 함수를 props로 넘길 때
    - `React.memo`와 함께 사용하여 렌더링 최적화할 
 **주의점**
    - 모든 함수를 `useCallback`으로 감싸면 오히려 성능 저하
    - 디버깅이 어려워질 수 있음


> **최적화는 필요할 때만**하며 Hook은 해당 병목이 확인된 경우에만 사용하는 것이 좋습니다.

##  마무리 요약

- 컴포넌트는 UI를 구성하는 기본 단위이며, 함수형이 현재 표준
- `useMemo`는 값 캐싱, `useCallback`은 함수 캐싱
- 둘 다 성능 최적화에 유용하지만, **남용은 독이 될 수 있음**