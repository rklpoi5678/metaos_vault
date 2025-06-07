## 핵심
Logcat은 안드로이드 시스템 및 앱에서 발생하는 로그 메시지를 출력하는 도구
로그 와 캣의 합성어로 유닉스 시스템에서 캣 명령어로 파일 내용을 출력하는 것처럼, 안드로이드 로그를 출력하는 데 사용된다.

## 기능
앱 디버깅, 시스템 상태 확인, 앱 성능 분석
기본적으로 터미널에서 그냥 치면 색상이 지정이 안되어있어서 가시성이 떨어진다는 단점이 있다.

adb logcat --pid=11429 -v long -v color 처럼 지정을 하면 각 속성마다 맞게 설정해준다.
or
adb logcat *:S ReactNative:V ReactNativeJS:V Expo:V
or
adb logcat AndroidRuntime:E
아니면 터미널에서
npx react-native log-android

> long: 모든 메타데이터 필드와 별도의 메시지를 빈 줄과 함께 표시
> brief: 메지지를 발그바는 프로세스의 우선순위, 태그 , PID를 표시
> color: 각 우선순위 수준을 다른 색상으로 표시한다.