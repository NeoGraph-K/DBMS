# DBMS 수업 자료
## DBMS 1일차
1. RDB 와 RDBMS
    1. 관계형 데이터 베이스 매니징 시스템
2. Table의 정의
    1. 데이터를 2차원 방식으로 구현한 자료 형태
3. SqlDeveloper를 이용한 Table 생성
    1. Create Table tablename (name type option, name type option, ...);
4. 자료형의 정의
    1. 데이터를 저장하기 위한 자료의 형태
5. DB의 자료형
    1. 숫자형
        1. number(n) n 자리수 설정
        2. number(n,m) n 자리수 m 소수점 설정
        3. 5 ~ 22byte
    2. 문자형
        1. char 고정 자리수 문자열
            1. 최소 1 최대 2000
            2. 나머지 스페이스
        2. nchar 고정 자리수 UTF-16
            1. 최소 1 최대 1000
        3. varchar2 가변 자리수 문자열
            1. 최소 1 최대 4000
        4. nvarchar2 가변 자리수 문자열 UTF-16
            1. 최소 1 최대 2000
        5. clob, nclob 대용량 텍스트
            1. 128TB
            2. 참조형
    3. 날짜/시간형
        1. Date
            1. 7 Byte
            2. 년/월/일/시/분/초
        2. TimeStamp
            1. 년/월/일/시/분/초/밀리초
        3. Interval
            1. 시간/틱
    4. 이진 데이터형
        1. 이미지,영상,음악,실행파일, ...
        2. blob 최대 128TB
6. 기본 옵션
    1. 기본 키
        1. Primary key
    2. 무조건 입력
        1. Not Null
7. 기본 데이터 입력
    1. Insert Into tablename(keyname, keyname2, ...) Values(data,data2,...);
8. 기본 데이터 조회
    1. Select * From tablename;
9. 트랜잭션
    1. Commit;
## DBMS 2일차
1. 사용자 생성 및 권한 부여
    1. CMD Oracle 접속
        1. CMD 실행
        2. sqlplus 입력
        3. 아이디 및 비밀번호 입력
    2. 사용자 생성 및 삭제
        1. 관리자 권한 접속
            1. conn/as sysdba
        2. 생성 및 삭제
            1. create user 유저이름 identified by 비밀번호
            2. drop user 유저이름 cascade
    3. 사용자 권한 부여 및 회수
        1. 모든 권한 주기
            1. grant connect, dba, resource to 유저
        1. grant 권한1, 권한2, ... to 권한유저
        2. grant 오브젝트권한 on 유저.테이블 to 권한유저
        3. revoke 권한1, 권한2, ... from 권한유저
        4. remove 오브젝트권한 on 유저.테이블 to 권한유저
        5. 권한 종류
            1. 시스템 권한
                1. create user - 유저 생성 권한
                2. create session - 접속 권한
                3. create table - 테이블 생성 권한
                4. create view - 뷰 생성 권한
                5. create any table - 모든 유저 테이블 생성 권한
                6. select any table - 모든 유저 테이블 조회 권한
                7. sysdba - DB 관리 최고 권한
                8. sysoper - DB 관리 권한
            2. 오브젝트 권한
                1. alter - 테이블
                2. index - 테이블
                3. insert - 테이블, 뷰
                4. select - 테이블, 뷰
                5. update - 테이블, 뷰
                6. delete - 테이블, 뷰
    4. 트랜잭션 적용
        1. commit;
    5. 유저 확인
        1. select * from all_users;
2. 테이블 생성
    1. create table 테이블이름(이름 타입(크기) 옵션, ...);
    2. 옵션
        1. Not Null - null 허용 여부
        2. default - 기본값
            1. age number(3) default 5
        3. unique - 중복 불가
        4. primary key - 기본 키
        5. check - 값 범위 지정
            1. age number(3,0) check (age >= 0)
            2. gender nvarchar2(2) check(gender in ('남성','여성'))
            3. percent number(6,2) check (percent between 0 and 100)
        6. references 다른테이블(다른테이블 primary key) - 참조한 테이블의 데이터만 삽입 가능
            1. on delete, on update 옵션
            2. no action - 참조테이블 변화와 상관 없음
            3. cascade - 참조테이블 변화시 동일 변화
            4. set null - 참조테이블 변화시 null
            5. set default - 참조테이블 변화시 기본값
    3. 제약조건 이름 지정
        1. constraint 제약조건이름 default (제약 칼럼)
        2. constraint 제약조건이름 unique (제약 칼럼)
        3. constraint 제약조건이름 primary key (제약 칼럼)
        4. constraint 제약조건이름 check (제약 칼럼 및 조건)
        5. constraint 제약조건이름 foreign key (제약 칼럼) references 다른테이블 (다른테이블 칼럼) on delete cascade
    4. 제약조건 조회
        1. select * from all_constraints where table_name = 테이블이름
    5. 코멘트
        1. comment on table 테이블명 is 코멘트 - 테이블 설명
        2. comment on column 테이블명.칼럼명 is 코멘트 - 칼럼 설명
        3. all_col_comments, user_col_comments, dba_col_comments - 코멘트 뷰
3. 테이블 변경
    1. alter table 테이블명 add(이름 타입(크기)) - column 추가
    2. alter table 테이블명 modify(이름 타입(크기)) - column 수정
    3. alter table 테이블명 drop column 이름 - column 삭제
    4. alter table 테이블명 rename column 이름 to 변경이름 - column 이름 변경
    5. alter table 테이블명 add constraint 제약이름 primary key (칼럼) - 칼럼 기본키
    6. alter table 테이블명 modify 칼럼 not null - 칼럼 null 비허용
    7. alter table 테이블명 add constraint 제약이름 unique (칼럼) - 칼럼 중복 비허용
    8. alter table 테이블명 add constraint 제약이름 foreign key (칼럼) references 다른테이블 (다른테이블 칼럼) - 외래키
    9. alter table 테이블명 drop constraint 제약이름 - 제약조건 삭제
4. 데이터 엑셀
    1. 추출
        1. select 질의문 데이터 검색
        2. 검색된 데이터 우클릭
        3. 익스포트
        4. 형식 - 엑셀
        5. 워크시트 - 파일위치
    2. 입력
        1. 테이블(필터링됨) 우클릭
        2. 데이터 임포트
        3. 찾아보기
        4. 파일 선택(.csv, .xls, .xlsx)
            1. 첫 행은 칼럼명
            2. ms949 인코딩(한글 안되면 변경)
        5. 변경할 테이블 이름
        6. 사용 가능한 열에서 필요한 열만 선택된 열로 이동
        7. 열의 데이터 타입과 크기 결정
## DBMS 3일차
1. 고유키
    1. 중복 불가능한 널 불가능한 식별키
2. 외래키
    1. 외부 테이블의 고유키로 참조하는 데이터키
    2. constraint 제약이름 foreign key(현재테이블칼럼) references 다른테이블(다른테이블칼럼)
    3. 테이블의 관계성을 유지하기 위한 칼럼
3. ERD
    1. 정보
        1. Entity Relationship Diagram
        2. E-R 다이어그램
        3. 테이블간의 관계에대한 도표
        4. A --------|- B 1:1
        5. A --------|= B 1:N(1<=)
        6. A -------O|- B 1:N(1>=)
        7. A -------O|= B 1:N
        8. 실선 - 부모의 기본키를 자식이 기본키로 쓰는 경우
        9. 점선 - 부모의 기본키를 자식이 기본키로 쓰지 않는 경우
    2. 사용법
        1. 보기 - Data Modeler - 브라우저
        2. 브라우저 - 관계형 모델(새 관계형 모델)
        3. 테이블 드래그
## DBMS 4일차