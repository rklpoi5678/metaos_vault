## 핵심
컴퓨터는 물리적인 진동이나 실제 영상이 뭔지 모른다. 컴퓨터는 단순히 숫자만 처리할 수 있다.
즉, expo-av는 이 숫자를 우리가 듣고 보는 실제 미디어로 바꿔주는 마법 같은 역할이다.

## 기능
- 소리를 재생하고, 중지하고, 볼륨을 조절할 수 있다.
- 비디오를 틀고, 멈추고, 속도를 조정
- 음악 플레이어나 동영상 플레이어를 코드로 직접 만드는 것과 같다.

## 예제 코드
```Tsx
import { Audio } from 'expo-av';

async function playSound() {
  const sound = new Audio.Sound();
  await sound.loadAsync(require('./audio.mp3')); // 파일을 불러와서
  await sound.playAsync(); // 재생하기!
}
```

## 요약
컴퓨터가 이해할 수 있는 숫자를 우리가 들을 수 있는 소리로 바꿔주는 도구다.
'소리를 듣고, 영상을 보는 것'을 가능하게 해주는 도구이다.

## 관련 라이브러리 차이점 정리
|라이브러리|기능|현재 상태|
|---|---|---|
|**expo-av**|오디오 및 비디오를 모두 지원|**더 이상 업데이트되지 않음 (Deprecated)**|
|**expo-audio**|오디오 전용 (음악, 효과음, 녹음 등)|**새로운 라이브러리로 대체됨**|
|**expo-video**|비디오 전용 (스트리밍, 재생, DRM 지원 등)|**새로운 라이브러리로 대체됨**|
> 새 프로젝트에는 expo-audio, expo-video 기존 expo-av를 사용중이라면 expo-audio,expo-video로 마이그레이션

