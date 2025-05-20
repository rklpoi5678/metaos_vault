
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


## 결론
Expo Managed Workflow -> AndroidManifest.xml을 직접 수정할 필요없다. 대신 app.json에서 설정 가능하다
Expo Bare Workflow -> 직접 AndroidManifext.xml을 수정 가능
