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
SHOW CREATE TABLE review;
-- 말그대로 이 테이블은 어떻게 만들어졌는지 sql문을 보여준다.
```

## 외래키로 보장되는 참조 무결성
```sql
# 영상에서 본 내용을 직접 확인해보세요.
ALTER TABLE review 
    ADD CONSTRAINT fk_review_table
    FOREIGN KEY (course_id)
    REFERENCES course(id)
    ON DELETE RESTRICT
    ON UPDATE RESTRICT;
    
/* review 테이블의 course_id 컬럼이 Foreign Key로 설정된 상태에서 
아래의 INSERT 문들을 실행해보세요.첫 번째 INSERT 문은 잘 실행되지만,
두 번째 INSERT 문은 참조 무결성을 위반하므로 에러가 발생합니다.*/

INSERT INTO review (course_id, star, comment)
    VALUES (8, 5 , '정말 좋은 수업이에요!');
    
INSERT INTO review (course_id, star, comment)
    VALUES (10, 5 , '정말 좋은 수업이에요!');
    
SELECT * FROM review;
-- 부모테이블인 coures id에는 10이라는 행이없는데 추가되면 참조무결성이 깨지게된다.
```

## 부모 테이블의 row가 삭제될 때 - RESTRICT 정책
![[Pasted image 20250927234457.png]]
> 만약 부모테이블의 해당 코스가 삭제될때 자식(부모를참조하고있는 테이블)을 어떻게 처리할것이냐
> 3가지 정책을 통해 설정할수있다.

RESTRICT는 삭제를 review테이블입장에서 참조하고있는  course로우를 삭제하지 못하게 아예 막아버린다. 즉, 참조하는 자식을 다지워야 부모의 그 로우를 삭제할수있다는 것이다.

>> NO ACTION: A keyword from standard SQL. In MySQL, equivalent to RESTRICT. The MySQL Server rejects the delete or update operation for the parent table if there is a related foreign key value in the referenced table. Some database systems have deferred checks, and NO ACTION is a deferred check. In MySQL, foreign key constraints are checked immediately, so NO ACTION is the same as RESTRICT.

no action와 restricet은 차이가 없다. 동일하다.
## 부모 테이블의 row가 삭제될 때 - CASCADE 정책
CASCADE: 는 폭포수처럼 떨어지다. 연쇄 작용을 일으키다.
부모 테이블을 지우면 그것을 참조하고 있던 자식도 연쇄 작용으로 삭제된다.
같이 삭제가된다.

## 부모 테이블의 row가 삭제될 때 - SET NULL 정책
부모테이블의 row가 삭제할때 그 참조되는 자식들의 외래키는 null이 되어버린다.
자식테이블의 대한 정보를 남겨눠서 , 전체 평균값을 계산하거나 그럴때 의미가있을때 사용할수있게 할수있다.

## 부모 테이블의 row에서 참조당하는 컬럼이 갱신될 때는?
ON DELETE 정책과 똑같다. id 값이 변경될때의 (갱신될때의) 정책이다.
```sql
/* 영상에서 본 내용을 직접 확인해봅시다
아래 ON UPDATE 부분에 매번 3가지 정책 이름을 적어보고 
각각 어떤 결과가 발생하는지 확인해보세요 */

ALTER TABLE review 
    ADD CONSTRAINT fk_review_table
    FOREIGN KEY (course_id)
    REFERENCES course(id)
    ON DELETE SET NULL
    ON UPDATE ???;
    

UPDATE course SET id = 100 WHERE id = 1;

/* 실행하기 버튼을 누를 때마다 실행기에서는 
기본 세팅된 테이블을 초기화하여 실행하기 때문에 
영상의 내용과 달리 아래 SQL 문은 실행할 필요가 없습니다.
UPDATE course SET id = 200 WHERE id = 100; */ 


# 각 정책별 실행 결과를 확인해봅시다 
SELECT * FROM review;
```
> RESTRICT: 부모 id가 변경시 제약
> CASCADE: 부모 id가 변경시 자식 외래키도 따라서 바뀐다.
> SET NULL: 부모  id가 변경시 자식의 외래키는 SET NULL

각 삭제나  갱신상황 각각 설정할수있어 실제에서는 상황에 따라 정책을 설정한다.