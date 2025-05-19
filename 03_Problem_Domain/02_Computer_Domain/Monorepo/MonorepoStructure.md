## 기본구조
```bash
Tool/ReactNative/
├── apps/
│   ├── guguTravel/            ←  개발은 여기서 함
│   │   ├── app.config.js      ← 앱 설정
│   │   ├── src/               ← 컴포넌트, 화면, 로직
│   │   └── ...
├── android/                   ←  빌드는 여기서 (prebuild 후 생성됨)
│   ├── app/
│   │   └── AndroidManifest.xml, MainActivity.kt 등
├── node_modules/
├── .npmrc
├── package.json
├── pnpm-workspace.yaml
└── ...

```

개발은 apps/에서, 빌드는 루트 Tool/ReactNative에서

## EXPO_TARGET_PROJECT_ROOT
루트 package.json에 스크립트 수정
```json
{
  "scripts": {
    "android:gugutravel": "cross-env EXPO_TARGET_PROJECT_ROOT=apps/guguTravel expo run:android"
  }
}

```

Window PowerShell/Command 환경일 경우
환경 변수 지정 방식이 다르므로 cross-env 사용

설치
pnpm add -D cross-env -w
> -w: --workspace-root 즉 루트 패키지의 package.json에 추가한다는것을 명시해주는것이다. 모노레포에서 실수로 앱 서브패키지 대신 루트에 dependency를 추가해버리는 것을 방지하려고 이렇게 만들었다.

실행
pnpm run android:gugutravel

## 앱설정
app.config.js or app.json 에서 entryPoint 환경변수로 진입점 명시
EXPO_TARGET_PROJECT_ROOT: 어느 앱을 실행할지 결정
루트애서 실행

"android:gugutravel": "cross-env EXPO_TARGET_PROJECT_ROOT=apps/guguTravel expo run:android"
> 모노레포 최상위 실행될 때 루트에서 환경 변수로 앱 폴더를 지정 Expo명령어를 실행 
> 모노레포 전반의 관점에서 한 번에 실행할 때 유용
> 다만 ../../App AppEntry.js 앱 진행지점을 못찾음(미해결)

"run:gugutravel": "pnpm --filter gugutravel run android"
> PNPM의 워크스페이스 필터 기능을 사용하여, 개별 패키지의 android스크립트를 실행한다.
## 개발중 빠르게
pnpm run start:gugutravel

## 앱을 기기에 직접 설치 하고 테스트
pnpm run android:gugutravel

## 프로덕션 빌드
eas build -p android --profile preview --project apps/guguTravel
> 실제 배포가능한 앱 빌드 파일(.apk, .aab, .ipa 등) 생성됨

빌드시간은 평균 3~10분
무료: 기본 요금제에서 월 30회 빌드 무료 (24년기준)