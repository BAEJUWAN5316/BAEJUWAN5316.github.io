# Post SQL 조작
<br>

## 1. 커넥션 만들기
1. vscode Post SQL 탭으로 접속
2. 우측상단 '+' 누르기
3. 127.0.0.1 입력
4. 'postgres'입력
5. '12345678'입력
6. 5432 적혀있는 그대로 엔터
7. 기본 아니면 미리 만들어 놓은 데이터베이스 클릭 또는 타이핑하고 엔터
8. 커넥션 이름 넣고 엔터
9. 만들기 완료
<br>
<br>

## 2. 데이터베이스 만들기
1. 커넥션 우측클릭 > New Query 누르기
2. 코드 작성
```SQL
CREATE DATABASE Juwan
```
3. 화면에서 우측클릭 후 Run Query 누르기
4. 오류가 없다면 database는 만들어졌다.
5. 하지만 화면에 표시되지는 않는다.
<br>
<br>

## 3. 테이블 만들기
1. 코드 작성
```SQL
CREATE TABLE juwan(
    id SERIAL PRIMARY KEY,
    title VARCHAR(100) NOT NULL
)
```
2. CRATE TABLE은 테이블을 만드는 명령어이다.
3. id라는 이름의 칼럼을 만들고, 속성은 SERIAL(자동으로 번호매기기), 키 속성의 뜻.
4. title이라는 이름의 칼럼을 만들고 속성은 VARCHAR(글자수 제한), NOT NULL(필수요소)라는 뜻.
5. Run Query 누르고 나면 데이터베이스 우클릭 > Refresh Items(새로고침) 눌러주면 생성된 테이블 확인 가능.
<br>
<br>

## 4. 테이블 CRUD
1. 테이블 이름 바꾸기
```sql
ALTER TABLE juwan
RENAME TO baejuwan;
```
- juwan이던 테이블 이름이 baejuwand으로 바뀐다

2. 데이터베이스 이름 바꾸기
```sql
ALTER DATABASE exam
RENAME TO Exam;
```
- exam으로 존재하던 데이터베이스 이름이 Exam으로 바뀐다
- 근데 이미 커넥션에 등록된 데이터베이스는 바꿀 수 없다
- 등록되지 않은 것만 가능!

3. 칼럼 추가
```SQL
ALTER TABLE juwan
ADD phone VARCHAR(11);
```
- 칼럼에 phone이 추가되었다.
- VARCHAR()은 글자 수를 제한하는 조건

4. 칼럼 삭제
```sql
ALTER TABLE juwan
DROP COLUMN phone;
```
- phone 칼럼이 삭제되었다.

5. 칼럼 이름 바꾸기
```sql
ALTER TABLE juwan
RENAME COLUMN title TO name;
```
- 칼럼명 title이 name으로 바뀌었다.

6. 칼럼의 조건 변경 - 글자 수 제한 변경하기
```SQL
ALTER TABLE juwan
ALTER COLUMN name TYPE VARCHAR(20);
```
- 글자수 제한이 20으로 바뀌었다!

7. 테이블 삭제하기
```SQL
DROP TABLE juwan;
```
- juwan 테이블이 삭제되었다.

8. 데이터베이스 삭제하기
```
DROP DATABASE exam;
```
- exam 데이터베이스가 삭제된다! 근데 열려있는 상태에서 하면 안 지워진다!
<br>
<br>

## 5. 데이터 CRUD
1. 값 테이블에 추가하기
```sql
INSERT INTO exam1 VALUES
(1, 'Pencil', 500);
```
- 데이터 테이블에 id=1, name='Pencil', price=500 인 값이 추가되었다.
- 근데 만약 들어 갈 값을 일정부분 지정해주고 싶다면
```sql
INSERT INTO EXAM1 (id, name) VALUES
(2, 'Note');
```
- 이렇게 해주면 id, name 값만 들어가고 price 부분은 null로 들어간다.

2. 조건을 걸어 값 변경하기
```sql
UPDATE exam1
SET price = price + 1000
WHERE id = 1;
```
- id가 1인 값의 price에 1000을 더해주겠다는 뜻이다.
WHERE 부분은 조건, SET 부분은 변경할 부분으로 보면 된다.
만약 조건 없이 전체의 값에 변경이 있다면
```SQL
UPDATE exam1
SET price = price + 50;
``` 
- WHERE을 생략하면 된다.

3. 데이터 지정해서 지우기
```sql
DELETE FROM exam1
WHERE id = 2;
```
- id가 2인 데이터가 지워졌다.

4. 데이터 갯수 세기
```sql
SELECT COUNT(*) FROM exam1;
```
- 카운트 된 숫자가 나온다.

5. 데이터 전부 지우기
```sql
DELETE FROM exam1;
```
- where이 없으면 전체가 지워진다.

6. 칼럼 추가와 함께 입력될 데이터 제한하기
```SQL
ALTER TABLE exam1
ADD gender VARCHAR(1) CHECK (gender IN ('F', 'M'));
```
- gender라는 칼럼을 추가하고, 여기에 'F', 'M' 둘 중 하나만 추가되도록 제한해줬다.

- 7. 특정 값 추출 조건 걸어서 데이터 추가하기
```SQL
SUBSTRING(id, 1, 1)
```
- id 칼럼에서 1번째 글자부터 1개 추출하겠다는 뜻!
만약 id의 값이 1234 이고 SUBSTRING(id, 2, 3) 이라면
234라는 값이 추출된다!
