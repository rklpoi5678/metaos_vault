## GitHub Workflow
GitHub Actions를 활용하여 정의, 코드 변경에 반응/ 특정조건에서 다양한 작업을 자동화 수행

## 워크플로우와 `YAML`파일
`.github/workflows` 디렉토리에 YAML파일 형식으로 저장

YAML(YAML Ain't Markup Language) 데이터를 구조화하는 데 사용되는 언어, json,xml과 같은 용도 YAML파일 형식은 구조와 규칙이 단순 -> 쉽게 읽고 수정

### **워크플로우 YAML 파일의 기본구성**
1. name: 워크프롤우의 이름
2. on: 어떤 이벤트에 워크플로우를 실행할지
3. jobs: 실행할 작업들을 정의하는 섹션, 각 작업은 여러 단으로 나눌수있다.

```yaml
# .github/workflows/example.yaml

name: Basic Workflow Example

on: [push]

jobs:
	example_job:
		runs-on: ubuntu-latest
		steps:
		- name: Checkout code
		  uses: actions/checkout@v3

		- name: Print Hello
		  run: echo "Hello, GitHub!"
```
> 이제 깃허브 액션에 보면 GitHub Workflow에 의해서 실행된 Actions 리스트를 볼수있다.

### **워크플로우 YAML 파일 돌아보기**
- ""