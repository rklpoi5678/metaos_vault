## course테이블과 review테이블 만들기
```sql
# 영상에서 배운 SQL문을 입력하고 실행해보세요
CREATE TABLE course (
    id INT NOT NULL AUTO_INCREMENT,
    title VARCHAR(30) NULL,
    semseter VARCHAR(6) NULL,
    maximum INT NULL,
    professor VARCHAR(10) NULL,
    PRIMARY KEY (id)
);

CREATE TABLE review (
    id INT NOT NULL AUTO_INCREMENT,
    course_id INT NULL,
    star INT NULL,
    comment VARCHAR(500) NULL,
    PRIMARY KEY(id)
);

# 실행 결과 확인용 코드
DESC course;
DESC review;
```

## Foreign Key가 필요한 이유
다른 테이블의 특정 컬럼을 식별할 수 있는 컬럼을 말한다. 우리말로 외래키라고 한다.
review테이블 중 특정 row가 나타내는 강의평가가 어느 수업에 대한 것인지 알려면
	(1) review테이블의 course_id 컬럼의 값을 보곡
	(2) course테이블로 가서 그 값의  id 컬럼의 값으로 가진 row를 찾으면 된다.
이런 경우를 보고 외래키가 주키를 참조(reference)한다라고 표현한다.

외래키가 존재할때 외래키가 있는 테이블을 자식테이블, 참조하는 테이블을 (referencing table)이라고 하고 참조되는 테이블을 부모테이블, 참조당하는  테이블(referenced table)이라고 한다.
이것이 다른 테이블의 컬럼을 참조하는 외래키다 라고 설정해 놓으면 참조 무결성(Referential Integrity) 라는것을 지킬수있다.

참조 무결성이란 두 테이블간 같은 참조 관계일때
각  데이터간에 유지되어야 하는 정확성과 일관성을 의미한다.
course_id 값이 3인 강의평가들은 있는데 정작 course 테이블에는 id값이 3인 수업이 없다??? 라는것은 참조 무결성이 훼손된 사례이다.

## 외래키 설정하기
```sql
ALTER TABLE `databaseName`,`review`
    ADD CONSTRAINT `fk_review_table`
        FOREIGN KEY (`course_id`)
        REFERENCES `databaseName`,`course` (`id`)
        ON DELETE RESTRICT
        ON UPDATE RESTRICT;
```

## SHOW CREATE TABLE 문으로 현재 테이블 어떻게 만들 수 있는지 보기
SHOW CREATE TABLE
	1. 실무에서도 유용하게 사용되는  SQL문
```sql
SHOW 
```
