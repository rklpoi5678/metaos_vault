## 핵심
웹사이트 + 인터렉티브한 요소 -> 프로트엔드
필요한 데이터 관리 + 프론트엔드에 전송 -> 백엔드

HTTP메소드 + URL = 엔드포인트라고하고
이것들의 모음을 API라고 한다. REST 스타일로 만들것이다.

node환경 (웹브라우저 바깥에서 자바스크립트를 실행하는 환경)
express (벡엔드 개발쪽에서 가장 유명한 라이브러리)
> 리퀘스트와 리스폰스를 쉽게 다룰수있음
> 다른 라이브러리(장고,스프링)에 비해 특정 구조를 고집하지 않고 최소한의 기능들만제공함

mongoDB (데이터를 테이블에 저장하지 않고 문서 형태로 저장)
문서하나 = 도큐먼트, 문서의 모음=컬렉션
셋업 과정도 간단하고 도큐먼트를 다루는 방법이 직관적임

## TODO API
**엔드포인트**
```node
GET /tasks
GET /tasks/:id
POST /tasks
DELETE /tasks/:id
PATCH /tasks/:id
```

**TASK 객체**
속성
\_id:string_
title: string
description: string
inComplete: boolean
createdAt: sting
updatedAt: string
```json
{
  "_id": "641bf3c9c0a964b65289902a",
  "title": "파이썬 공부",
  "description": "프로그래밍 시작하기 in Python 토픽 끝내기",
  "isComplete": false,
  "createdAt": "2023-03-23T06:34:11.617Z",
  "updatedAt": "2023-03-23T06:34:11.617Z"
}
```

## PATCH vs PUT
수정시 PUT 메소드도 많이사용
PATCH는 데이터를 부분수정할때, 리퀘스트 바디로 전달되는 필드들만 수정하는것
반면 PUT은 데이터를 아예 새로운 데이터로 덮어쓸 때 사용한다.
리퀘스트 바디로 아예 덮어쓸 데이터(객체)를 전달해야한다.

