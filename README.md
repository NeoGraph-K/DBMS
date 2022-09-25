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
1. 데이터 삽입
    1. insert into 테이블(칼럼명1,칼럼명2, ...) values(데이터1,데이터2,...);
    2. insert into 테이블 values(데이터1,데이터2,...);
    3. insert all when 조건 then into 테이블1 values(데이터1,데이터2,...) else into 테이블2 values(데이터1,데이터2,...) 서브쿼리(select 칼럼 from 테이블 where 조건);
    4. insert first when 조건 then into 테이블1 values(데이터1,데이터2,...) else into 테이블2 values(데이터1,데이터2,...) 서브쿼리(select 칼럼 from 테이블 where 조건);
2. 데이터 검색
    1. select 칼럼 from 테이블;
    2. select 테이블1.칼럼, 테이블2.칼럼 from 테이블1,테이블2;
    3. select 칼럼 as 칼럼새이름 from 테이블;
    4. select 칼럼 from 테이블 order by 칼럼명 ASC(오름) or DESC(내림);
    4. select 칼럼 from 테이블 where 조건절;
        1. 칼럼 = 값 - 특정 값 검색
        2. 칼럼 != 값 - 특정 값 제외 검색
        3. 칼럼 is null - 특정 값 없는 데이터 검색
        4. 칼럼 is not null - 특정 값 비어있지 않는 데이터 검색
        5. 칼럼 like 값 - 문자열 비교 검색
            1. % - 0개 이상 아무 글자
            2. _ - 1개 아무 글자
        6. 칼럼 (>,<,!=,<>,<=,>=) 값 - 비교 검색
        7. 칼럼 between 값1 and 값2 - 사이값 검색
        8. 칼럼 in(값1, 값2) - 특정 값 목록 검색
        9. select distinct 칼럼 from 테이블 - 중복 제외
        10. 조건절 and 조건절 - 모든 조건절 만족 데이터 검색
        11. 조건절 or 조건절 - 모든 조건절 불만족 데이터 제외 검색
        12. exists (서브쿼리) - 서브쿼리문의 데이터가 존재하면 True
        13. not exists (서브쿼리) - 서브쿼리문의 데이터가 없으면 True
3. 데이터 삭제
    1. delete from 테이블 where 조건절;
4. 데이터 수정
    1. update 테이블 set 칼럼1 = 데이터1, 칼럼2 = 데이터2, ... where 조건절;
## DBMS 5일차
1. 함수
    1. 문장 함수
        1. lower(문장) - 모두 소문자
        2. upper(문장) - 모두 대문자
        3. initcap(문장) - 첫글자 대문자 나머지 소문자
        4. cancat(문장1,문장2) - 두개의 문장을 연결, || 와 동일 기능
        5. substr(문장,시작,개수) - 문자중 일부를 잘라내기
        6. length(문장) - 문장의 길이
        7. nvl(칼럼,디폴트) - 칼럼이 NULL이면 디폴트
        8. nvl2(칼럼, 디폴트1, 디폴트2) - 칼럼이 not null 이면 디폴트1 null 이면 디폴트2
        9. rtrim(문장, 옵션) - 오른쪽의 공백문자 제거 또는 옵션의 반복문자 제거
        10. ltrim(문장, 옵션) - 왼쪽의 공백문자 제거 또는 옵션의 반복문자 제거
        11. trim(문장) - 양쪽의 공백문자 제거
        12. rpad(문장, 길이, 문자) - 길이만큼 공간에 문장 채우고 빈 오른쪽을 문자로 채움
        13. lpad(문장, 길이, 문자) - 길이만큼 공간에 문장 채우고 빈 왼쪽을 문자로 채움
        14. translate(원본문장,변환문장1,변환문장2) - 원본문장에서 변환문장1에 있는 글자를 변환문장2에 같은 위치에 있는 문자로 변환 변환문장2가 더 짧으면 모자란 글자는 제거
        15. replace(문장, 찾을문장, 변환문장) - 원본문장에서 찾을 문장을 변환 문장으로 변환
        16. intstr(원본문장, 찾을문장, 찾기 시작할 글자 위치, 찾을 결과의 순번) - 원본문장에서 찾을문장의 위치, 찾기 시작할 글자 위치를 -(마이너스)를 통해 뒤부터 찾기 가능
    2. 숫자 함수
        1. round(실수,자리수) - 자리수가 양수이면 해당 자리수 아래에서 반올림, 자리수가 음수이면 해당 자리수에서 반올림, 날짜도 가능
        2. trunc(실수,자리수) - 자리수가 양수이면 해당 자리수 아래에서 절사, 자리수가 음수이면 해당 자리수에서 절사
        3. mod(정수1,정수2) - 정수1을 정수2로 나눈 나머지
        4. abs(숫자) - 절대값
        5. sign(숫자) - 음수는 -1 양수는 1 0은 0
        6. floor(실수) - 내림
        7. ceil(실수) - 올림
        8. power(숫자,지수) - 숫자의 지수 제곱
        9. log(지수,숫자) - 로그 값
        10. sin(라디안각도) - 사인값 - 3.1415926535 / 180 * 디그리 각도
        11. cos(라디안각도) - 코사인값
        12. tan(라디안각도) - 탄젠트값
    3. 날짜 함수
        1. sysdate, systimestamp from dual - 현재 시스템 날짜
        2. add_months(날짜, 숫자) - 숫자만큼 날짜에 개월수를 더한 날짜
        3. last_day(날짜) - 해당 날짜의 달의 마지막 일
        4. new_time(날짜, 타임존1, 타임존2) - 날짜를 타임존1에서 타임존2 날짜로 변환
            1. AST, ADT
            2. BST, BDT
            3. CST, CDT
            4. EST, EDT
            5. GMT
            6. HST, HDT
            7. MST, MDT
            8. NST
            9. PST, PDT
            10. YST, YDT
        5. next_day(날짜, 요일) - 해당 날짜 다음으로 해당 요일이 오는 날짜
            1. 1, 일요일, 일, sunday, sun
            2. 2, 월요일, 월, monday, mon
            3. 3, 화요일, 화, tuesday, tue
            4. 4, 수요일, 수, wednesday, wed
            5. 5, 목요일, 목, thursday, thur
            6. 6, 금요일, 금, friday, fri
            7. 7, 토요일, 토, saturday, sat
        6. months_between(날짜1, 날짜2) - 두 날짜 사이의 개월수
    4. 변환 함수
        1. 형식 요소
            1. MM - 달수
            2. MON - 월 축약
            3. MONTH - 월 풀네임
            4. DD - 날짜
            5. D - 주의 일수
            6. DY - 요일 축약
            7. DAY - 요일 풀네임
            8. YYYY - 날짜 4자리
            9. YY - 날짜 마지막 2자리
            10. 9 - 숫자(9999->1234)
            11. 0 - 자리수 빈공간 0(09999->01234)
            12. $ - 금액에 $표시($999->$123)
            13. . - 위치에 소수점(999.9->123.4)
            14. , - 위치에 쉼표(999,999->123,456)
        2. to_char(숫자 or 날짜, 형식) - 숫자나 날짜를 문장으로 변환
        3. to_number(문장) - 숫자를 포함하는 문장을 숫자로 변환
        4. to_date(문장, 형식) - 문장을 날짜로 변환
## DBMS 6일차
1. 집계 함수
    1. SUM - 칼럼 총합
    2. MAX - 칼럼 최대
    3. MIN - 칼럼 최소
    4. AVG - 칼럼 평균
    5. COUNT - 칼럼 개수
2. Group By
    1. select 중복칼러명(group by 지정 칼럼), 집계 칼럼 from 테이블 group by 중복칼럼;
    2. 동일 칼럼끼리 그룹화
3. Having
    1. select 중복칼럼명(group by 지정 칼럼), 집계 칼럼 form 테이블 group by 중복칼럼 having 집계 조건절;
    2. 집계 함수를 이용한 조건 검색 가능
4. 검색 순서
    1. select 칼럼 from 테이블명 where 데이터 조건절 group by 데이터 그룹화 칼럼명 having 집계 조건절;
5. 집합
    1. UNION - 합집합
        1. select * from 테이블 union select * from 테이블; - 중복 제거
        2. select * from 테이블 union all select * from 테이블; - 중복 비제거
    2. INTERSECT - 교집합
        1. select * from 테이블 intersect select * from 테이블;
    3. MINUS - 차집합
        1. select * from 테이블 minus select * from 테이블; - 앞 테이블 검색 결과에서 뒤 테이블 검색 결과 제외
6. CASE 조건
    1. 오라클에는 DECODE가 있지만 CASE가 가독성이 뛰어나며 다른 곳에서도 호환성이 뛰어남
    2. IF 문
        1. select case when 조건절 then 결과 when 조건절 then 결과 else 결과 end as 칼럼별명 from 테이블명;
        2. else 생략 가능 생략시 조건 결과가 없으면 NULL
    3. SWITCH 문
        1. select case 칼럼명 when 조건값 then 결과 when 조건값 then 결과 else 결과 end as 칼럼별명 from 테이블명;
        2. 단순 값만 비교시 훨씬 뛰어난 가독성
    4. where 절에서도 사용 가능
    5. 내장 함수를 조건절로 사용 가능
    6. then 결과절에 중첩으로 case 사용 가능