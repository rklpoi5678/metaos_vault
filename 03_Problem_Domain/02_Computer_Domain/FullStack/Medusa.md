



### 서비스 팩토리
Medusa는 모듈의 주요 서비스가 확장할 수 있는 서비스 팩토리를 제공한다.
데이터베이스의 데이터 모델에 대한 데이터 관리 메서드를 생성하므로 이러한 메서드를 수동으로 구현할 필요가없다

```javascript
import { MedusaService } from "@medusajs/framework/utils"
import Post from "./models/post"

class BlogModuleService extends MedusaService({
  Post,
}){
consturctor(){
	super(...arguments)
}
  // TODO implement custom methods
}

export default BlogModuleService
```
### MedusaService 매개 변수
데이터 관리 메서드를 생성할 데이터 모델의 개체인 하나의 매개 변수를 허용
서비스를 구현하는 경우 이를 전달하여 호출 해야 한다.