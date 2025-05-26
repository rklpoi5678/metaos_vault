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

