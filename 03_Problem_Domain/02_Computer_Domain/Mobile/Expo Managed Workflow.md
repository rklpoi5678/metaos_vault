
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

## 결론
Expo Managed Workflow -> AndroidManifest.xml을 직접 수정할 필요없다. 대신 app.json에서 설정 가능하다
Expo Bare Workflow -> 직접 AndroidManifext.xml을 수정 가능
