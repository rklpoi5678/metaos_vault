
## 핵심
빌드가 서버에서 가능
expo-go 제약 -> dev client 따로 빌드 필요하다
CLI는 편하지만, 네이티브 커스터마이징에 약하다
결국 초기 진입은 빠른데 , 중후분은 느린단점

## 특정 권한을 추가하고 싶다면?
app.json파일에 android.permissions 항목을 설정하면된다.
예 위치권한
```json
{
	"expo": {
		"android":{
			"permissions": ["ACCESS_FINE_LOCATION"]
		}
	}
}
```
이러헤 설정하면 Expo가 자동으로 AndroidManifest.xml을 생성하고 해당 권한을 포함시켜준다.

## 환경변수 넣기
eas env:push(환경변수용으로 통합됨)
모든 환경변수 목록 보기: eas env:list
특정값 수정하기 eas env:push YOUR_VAR=new_value
환경 변수 삭제: eas env:delete  GOOGLE_ANDROID_GEO_API_KEY

예:eas env:push  --environment development 
(.env내용이없을시 프롬프트창이뜨면서 키/밸류값 입력이 나오고,
있을시 .env내용이 EAS환경에 업로드된다.)

| 옵션                     | 설명                                             |
| ---------------------- | ---------------------------------------------- |
| `--environment` (`-e`) | `development`, `preview`, `production` 중 하나 필수 |
### 다른 keystore
로컬빌드시
EAS 빌드가 쓰는 keystore는 expo run:android와 다를 수 있다.
eas credentials -> Build Credentials에서 SHA-1 Releas 지문을 복사해서
Cloud Console -> API & Services -> Credentials -> "Android 앱제한"에 추가
[Finger Print]

프로덕션빌드시
EAS 환경변수에 실 ID등록 (eas secret:push)
eas secret:push --name EXPO_PUBLIC_GOOGLE_MOBILE_ADS_APP_ID --value "ca-app-pub-5223844528723811~4155309336"
eas secret:push --name EXPO_PUBLIC_GOOGLE_IOS_ADS_APP_ID --value "ca-app-pub-5223844528723811~4155309336"
eas secret:push --name EXPO_PUBLIC_GOOGLE_ANDROID_GEO_API_KEY --value "AIzaSyD8hR1hWUPqC17a20FlZ6p8K7RLFLWH8b0"

`eas secret:push` 명령어는 Expo의 EAS CLI 도구에서 제공하는 기능으로, 로컬에 있는 환경 변수 파일(예: `.env`)에서 비밀 정보를 읽어 Expo 빌드 서버에 안전하게 저장하는 역할을 합니다. 이를 통해 API 키나 기타 민감한 데이터를 소스 코드에 직접 포함시키지 않고도 빌드 환경에 주입할 수 있습니다.
This command is deprecated. Use eas env:push instead.(참고)

### eas env:* 와 eas secret:push 차이 
secret:push는 오직 민감한 비밀 정보만을 위해 설계되었다. 단순히 빌드 시점에 주입된다.
env:push는  민감한 정보(비밀)뿐 아니라 공개해도 되는 일반 환경 변수까지 포함, 프로젝트에서 사용하는 모든 환경 변수를 통합적으로 관리할 수있다. 개발->미리보기->프로덕션 등 여러 환경에 맞게 별도로 값을 설정하고 관리할수있다.

다음은 명령어 사용법과 각 옵션에 대한 설명입니다:

환경변수 삭제법
eas env:delete production --variable-name EXPO_PUBLIC_SUPABASE_URL
eas env:delete production (대화형 프롬프트제공됨 --non-interactive사용시 제외)

## 배포&빌드&테스트

| 상황               | 추천 방법                                                  | 명령어                          |
| ---------------- | ------------------------------------------------------ | ---------------------------- |
| 단순 빠른 `.apk` 테스트 | ✅ `expo run:android`                                   | `pnpm exec expo run:android` |
| dev client 테스트   | ✅ `eas build --local -p android --profile development` | + `buildType: apk`           |
| CI나 배포도 고려       | `eas build -p android --profile preview`               | + `buildType: apk`           |
오류 디버깅용
>adb logcat *:S ReactNative:V ReactNativeJS:V Expo:V

apk 설치
> adb install -r build-\*.apk

### eas.submit이있다면 
eas.json 설정 후  내부 테스트(internal) 트랙으로 업로드
eas build --profile preview --platform android (클라우드 이용)
 최신 빌드 파일(.aab) ID를 자동 검색해 제출
eas submit --profile preview --platform android --latest
### 로컬 eas.submit
로컬로 할시 .aab파일을 구분하기 쉽게 폴더로 넣고
eas submit -p android --track internal --service-account-key ./google-service-account.json --path ./build/app-release.aab
 
 or 빌드가 끝난 .aab를 Google Play Console에 제출
pnpm exec eas submit --platform android --profile production --path dist/*.aab

### 로컬이 더빠르긴 하다.
왜 원격 빌드가 더 느리게 느껴질까나?

### 환경변수 확인
eas env:exec \[ENVIRONMENT\] \[Bash Commend(키값)\]
으로 빌드전 환경변수가 로드되었는지 확인해볼수있다.

EAS 서버의 환경 변수를 로컬.env로 가져올 수 있다. eas env:pull
민감한 키는 .env에 넣어두고 eas.json에는 삽입금지
Secret값은 Gradle,IOS의 Info.plist에만 주입되며 Google Maps Android API같은 키들은 민감한데 이것들은 Gradle이나 Info.plist에 설정된 API키를 통해 인증하고 작동하기때문에 Secret값으로 넣어두면 네이티브 세팅에 올바르게 주입되어 앱 내에서 지도 기능이 정상적으로 작동한다.

환경변수는 빌드 프로세스 중에 정적으로(하드코딩된 값으로) 번들에 포함된다. 한 번 빌드가 완료되면 그 빌드 결과물은 그 시점의 환경 변수 값으로 고정된다. 따라서 변경 사항을 앱에 반영하려면 새로운 빌드를 수행하여야 한다.
## 결론
Expo Managed Workflow -> AndroidManifest.xml을 직접 수정할 필요없다. 대신 app.json에서 설정 가능하다
Expo Bare Workflow -> 직접 AndroidManifext.xml을 수정 가능
