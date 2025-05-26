## 핵심
React Native Expo에서 색상을 부드럽게 변화시키는 기능을 제공
여러 색상을 지정하면, 그 사이에서 자연스럽게 혼합된다.
사용자는 시작 색, 끝 색, 방향을 정해서 원하는 효과를 만들 수 있다.

```Tsx
import { LinearGradient } from 'expo-linear-gradient';

export default function GradientExample() {
  return (
    <LinearGradient
      colors={['blue', 'orange']} // 시작 색과 끝 색 설정
      start={{ x: 0, y: 0 }}      // 시작 위치 (왼쪽 상단)
      end={{ x: 1, y: 1 }}        // 끝 위치 (오른쪽 하단)
      style={{ width: 200, height: 200 }}
    />
  );
}
```

## 요약
색상을 자연스럽게 연결해서 보기 좋게 만드는 도구다. 붓으로 색을 섞듯이, 디지털 화면에서도 부드러운 색 변화를 만들 수 있는 도구이다.