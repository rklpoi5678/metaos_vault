## 핵심
화면에 부드러운 움직임을 원하지만, 내부적으로는 JS(JavaScript)와 네이티브 코드(장치에서 직접 실행되는 코드)가 서로 데이터를 주고받으며 처리하는 방식이다.

## 문제
JS가 모든 프레임마다 애니메이션을 계산해서 네이티브 코드로 보내야 한다면? 너무 많은 데이터 이동 때문에 애니메이션이 느려질 수 있다.(JS 스레드가 너무 바빠지고 화면이 끊길 수도 있다.)

## 그래서 useNativeDriver
여기서 등장하는 해결책이 useNativeDriver:true JS가 애니메이션을 매번 계산하는 대신 처음부터 네이티브 코드에 "이렇게 움직여!"하고 직접 명령을 내려버림

```Tsx
Animated.timing(fadeHeight, {
  toValue: 1,
  duration: 10000,
  useNativeDriver: true,  // 네이티브 드라이버 활성화!
}).start();
```
