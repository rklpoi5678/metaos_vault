
## 설명
앱의 메타데이터 설정 (앱 이름, 아이콘, extra등)
즉, 앱의 "외부 껍데기" 정보를 담고있다 (버전,splash, 환경변수 등등)
빌드, 실행 시 자동 파싱된다.
## 사용상황
React Native + Expo
## eas.json 
EAS 빌드/ 업데이트 관련 빌드 전략/ 프로파일 설정
eas build, eas update 같은 EAS 명령어 쓸 때만 사용된다.
CI/CD, 릴리즈 전략 구분용
Expo가 아니라 React Native 만 쓴다면 -> eas.json 필요 없다.

## Expo Go만 쓴다면?
eas.json 없어도 되고 expo start + app.json or app.config.js로 충분하다/

## Dev Client + OTA 업데이트 등 EAS 전체 활용할 거라면?
eas.json + app.config.js 둘 다 필요
eas.json은 빌드 전략
app.config.js는 앱 정보와 런타임 환경변수