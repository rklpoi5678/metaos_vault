## 핵심
소프트웨어로 건물을 짓는 건축 관리자
집을 짓기 위해 해야 할 여러 작업들을 미리 계획해서 정리해준다.

## 비유
- 작업(Task): 벽돌쌓기,창문설치, 전선 연결등 각기 수행할 작업들을 의미
- 의존성(Dependency): 어떤 작업은 다른 작업이 완료되어야 시작하는데 글래드는 이러한 순서를 알아서 관리한다.
- 자동화: 글래드는 미리 작성해둔 스크립트를 따라 자동으로 이 모든 작업을 수행해준다
> 코드와 자재들을 조합해 실행 가능한 프로그램(완성된 집)을 만드는데 그 전체 과정을 자동화하고 관리하는 도구이다. 복잡한 과정을 자동으로 처리하고 효율적으로 처리하여 잘못된 순서나 누락 없이 앱을 빌드할수있다.

### autolinking
React Native(및 Expo)에서 네이티브 모듈들을 수동으로 연결할 필요없이, 자동으로 프로젝트에 통합할 수 있도록 해주는 메커니즘이다.

Gradle이 프로젝트의 node_modules디렉토리를 스캔하여, 설치된 Expo or ReactNative 모듈중 네이티브 코드가 포함된 라이브러리들을 자동으로 링크한다.
```Gradle
apply from: new File(
    ["node", "--print", "require.resolve('expo/package.json')"].execute(null, rootDir).text.trim(),
    "../scripts/autolinking.gradle"
);
useExpoModules()
```
> 필요한 기능들을 빠르게 사용할 수 있게 되는것이 바로 autolinking의 이점이다
> 프로젝트 설정과 통합 과정을 간소화하여 개발자가 네이티브 링크 관련 수동 작업에 신경 쓰지 않고, 앱 개발에 집중할 수 있도록 도와줌

## AGP

자동차 공장을 운영하는 로봇 시스템
코드가 원재료, AGP는 공장 관리자 역할, Gradle이 조립라인, 출고 전 검증
AGP는 안드로이드 앱을 빌드하는 자동화 엔진이며, Gradle과 함께 작동하여 코드를 실행 가능한 앱 파일로 변환하는 핵심도구이다.

## JVM 메모리 늘리기
# 이미 있다면 값만 덮어쓰기
org.gradle.jvmargs=-Xmx6g -Dfile.encoding=UTF-8 -XX:+UseParallelGC \
                   -XX:+HeapDumpOnOutOfMemoryError

# Kotlin 컴파일러용(필수 아님, 여유 있으면 추가)
kotlin.daemon.jvmargs=-Xmx2048m
