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
- "Basic Workflow Example"
- push 이벤트 발생시 실행
- 하나의 작업인 example_job이 정의됨
	- 이값은 YAML 파일의 규칙이 허용하는 선에서 원하는대로 변경가능
- 이 작업은 ubuntu-latest환경에 실행
	- runs-on 속성을 통해 어떤 환경에서 실행할지 결정가능, 이 속성을 runners라고 부릅니다.(깃허브에서는 해당러너들을 무료로 이용할수있게함)
	- 우분투 이외 다른 OS를 runs-on으로 설정가능
- 이 작은은 repository를 clone한 후 해당 브랜치로 checkout을 수행, 이후 Hello.... 출력
	- 액션에서 스탭은 각작업(job)내 실행단계를 나타냄
	- step모음을 job을 구성, step은 순차실행 그 이후 스텝은 기본적으로 실행되지않음

## step 속성
1. name: step이름, 액선로그에 표시, 의미 있는 이름으로 로그를 쉽게읽게하기
2. run: 해당 step에서 실행할 shell,스크립트 지정 runnersOSd에 직접명령수행
3. uses: 특정 액션을 사용하도록 지정
4. with