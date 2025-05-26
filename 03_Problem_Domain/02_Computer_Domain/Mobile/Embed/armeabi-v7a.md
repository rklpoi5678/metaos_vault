
## 핵심
Android 기기의 CPU아키텍쳐 중 하나로 , 주로 저사양 혹은 32비트 ARM기반 디바이스에서 사용됨

## 비유
armeabi-7ba는 오래된 32비트 엔진을 가진 스마트폰
arm64-v8a는 더 강력하고 최신의 64비트 엔진을 가진 스마트폰

앱을 배포할때 이 CPU엔진에 맞춰 앱을 최적화해야함, armeabi-7ba지원을 제거하면 오래된 32비트 스마트폰에서는 앱이 실행되지 않을수있다.
반대로 arm64-v8a 전용으로 개발하면 최신 디바이스 에서 더 빠르게 작동할수있다.

즉, 스마트폰 CPU의 한종류이며, 저사양 혹은 32비트 기기에 맞춘 앱 실행 환경이다.

## 빌드시
expo-modules-core의 일부 네이티브 C++ 구성 요소들은 armeabi-v7a로 빌드할때 build.ninja 캐시 로직이 꼬이는 현상이 자주 발생

.cxx(및 캐시삭제)를 삭제해도 dirty after 100 tries 오류가 반복적으로나온다면 armeabi-v7a제거를 한다.
dev-client에서 64비트만으로 충분

Google Play에서는 64비트 지원을 필수로 요구하며 최신 앱은 armeabi-v7a를 지원하지 않을 수 있다.


### powershell 명령어
Remove-Item -Recurse -Force "C:\Users\PW1234\Desktop\Tool\ReactNative\node_modules\.pnpm\expo-modules-core@2.3.13\node_modules\expo-modules-core\android\.cxx"