
## Expo Go
Expo 팀에서 미리 빌드해 배포한 공식 클라이언트 앱
특별한 추가 네이티브 구성이 없어도 Expo 프로젝트를 빠르게 실행 할 수 있게 설계

### 제한 사항
Expo Go 는 Expo SDK에 포함된 네이티브 모듈들만 지원 따라서 사용할 수 없는, 혹은 커스텀 네이티브 모듈을 사용하려면 제약이존재

## Custom Dev Client (Expo Dev Client)
필요한 커스텀 네이티브 코드나 추가 모듈을 포함하여 직접 빌드하는 개발 클라이언트이다.
EAS(Build)을 통해 클라우드에서 직접 빌드해서 만들어내며, 기본 Expo GO 대신 사용

## 장점
커스텀 네이티브 모듈들을 앱에 추가 가능, 이를 통해 Expo프로젝트에 Expo SDK이 상으로 필요한 네이티브 기능을 테스트하고 개발가능

프로젝트에 맞게 커스터마이징되므로, 별도의 빌드 과정(EAS Build 등)이 필요하며, 빌드 한 후 해당 클라이언트를 디바이스에 설치하여 사용한다.


## 비유
공장에서 미리 만들어진 범용 리모컨 -> Expo Go
리모컨에 없는 특별한 기능은 사용할 수 없다. 

반면 Custom Dev Client는 직접 부품을 추가해 맞춤형 리모컨을 만드는것이다.

커스텀이 필요할때는 CDC
기본 EXPO -> EXPOGO

## 결론
처음부터 지도, 애드몹, 위치, 네이티브 연동이 많은 앱은 Expo Go는 너무 제한적이라 진짜 개발에서는 못쓴다.

`AdMob`, `Map`, `Camera`, `Push`, `Location`, `sqlite`, `reanimated`, `gesture-handler` 등 하나라도 있으면 무조건 **Expo Go 탈출**

dev client 한 번 설치 후
pnpm exec expo run:android

이후 개발 시
pnpm exec expo start --dev-client
-> 코드는 빠르게 반영되고 실제 환경에서 테스트 가능

배포 전 빌드
pnpm exec eas build -p android

