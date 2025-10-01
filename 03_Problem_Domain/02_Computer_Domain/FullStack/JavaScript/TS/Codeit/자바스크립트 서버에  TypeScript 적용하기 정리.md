## 타입스크립트 적용하기 정리
패키지 설치: @types, npm사이트 찾기, 타입스크립트를 지원해준다면 따로 설치할필요가없다.
## Express 핸들러 타입
Request,Response,NextFunction
RequestHandler

## 타입 커스텀
 외부 모듈에 대해 declare문법을 활용하면 타입을 덮어쓸수있음, interface 문법의 경우 이미 정의된 interface와 합쳐지기 때문에 내가 원하는 특정  프로퍼티는 아래와 같이 간단히 추가해볼수있다.
 ```ts
 // express.d.ts
 import Express from  'express';
 
 declare global
 ```