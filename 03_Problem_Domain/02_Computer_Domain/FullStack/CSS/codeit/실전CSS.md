## 작업 계획하기

1. 디자인 살펴보기: 피그마 -> 전체적인레이아웃 나누기(헤더,섹션) -> 반응형디자인 살피기
	1. 디자인 -> 데스크톱, 데스크톱 -> 모바일  먼저 시작점을 무엇으로 스타트할꺼냐에  따라 편하기가 갈림
	2. 피그마에서 Design > Export 메뉴에서 이미지 파일다운 > png면 favicon (.ico 변환) > 다른 이미지들도 다운

## 작업 순서 정하기
정리
1. 공통 HTML, CSS 준비
	1. HTML 기본 코드 생성
	2. 페이지 아이콘 적용
	3. 폰트 적용하기
	4. 공통 CSS 적용하기
2. 홈페이지 구현 (먼저 html요소를 꾸며주고 정의하는게 더 빠름)
	1. 레이아웃 나누기
	2. 헤더 구현
	3. 설문 조사 목록 구현
3. 컬러 등록 페이지 구현 (각 섹션별로 먼저정의 하나 섹션끝난후 확인 라이브 서버체크하면 편함)
	1. 제목
	2. MBTI 입력부
	3. 컬러 입력하는 부분
	4. 컬러 등록하는 부분
4. 반응형 디자인 적용
	1. 모바일 홈페이지에서 헤더의 레이아웃 변경하기
	2. 모바일에서 글자 크기, 간격 변경하기

### **팁**
아이콘, 이미지가 너무작다 x3(3배수이상) 기본 2배이상 이미지를 다운받아 픽셀이 최대한 안깨지도록 작업

##  1번
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  
</body>
</html>
<!-- 이러한 기본 코드부터 먼저 정의 -->
```
```html
<!-- 페이지 아이콘 적용하기 -->
<link rel="icon" href="favicon.ico">
```

```html
<!-- 폰트 적용 -->
<link rel="stylesheet" as="style" crossorigin href="...">
```
```CSS
/* 공통 css 작성 */

/* CSS 작업을 편하기위해 보더박스 적용 */
* {
	box-sizing: border-box; 
}

/**
*  폰트와 기본 글자 색, 기본 글자 크기 정하기
* 폰트는 특수폰트(웹폰트)지정 없으면 sans-serif
* 피그마 디자인에서 공통적인요소 (ex: 글자색 #464e5e 글자크기24px 가 공통이었다.)
*/

html {
	font-family: Pretendard, sans-serif;
	font-size: 24px;
	color: #464e5e
}

/* body에는 마진 값없애기 */

body {
	margin: 0;
}
```

1번 정리코드
```html
<!DOCTYPE html>
<html lang='ko'>
<head>
	<meta charset='UTF-8'>
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>MBTI별 좋아하는 컬러</title>
	<ㅣㅑㅜㅏ

</head>
```