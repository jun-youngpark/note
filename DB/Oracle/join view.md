# 수정 가능 조인 뷰
1. /*+ BYPASS_UJVC */
   - Oracle 11g 부터 사용할 수 없는 힌트 임.
   - 키-보존이 안되서 나는 오류를 무시하라는 힌트.

	UPDATE /*+ BYPASS_UJVC */
   ( SELECT A.GBN AS A_A
 , B.GBN AS B_B
   FROM MAIN A
    INNER JOIN STEP B
    ON A.ID = B.ID
 WHERE A.TIME='01'
   ) X
	  SET X.A_A = X.B_B
	;

2. ORA-01779: 키-보존된것이 아닌 테이블로 대응한 열을 수정할 수 없습니다
   (ORA-01779: cannot modify a column which maps to a non key-preserved table)
   - 키보존 되도록 하려면 B테이블의 ID 컬럼을 PK, UK로 셋팅 해야 함.
     (Unique함을 보증)

3. 다른 방법
   1) Sub-Query
 UPDATE MAIN A
    SET GBN = (SELECT GBN FROM STEP B WHERE B.ID = A.ID)
 WHERE A.TIME = '01'
    AND EXISTS (SELECT 1 FROM STEP B WHERE B.ID = A.ID)
 ;
   2) Merge
 MERGE INTO MAIN A
      USING (SELECT A.ID, B.GBN FROM MAIN A, STEP B WHERE A.ID = B.ID AND A.TIME='01') C
         ON (A.ID = C.ID)
 WHEN MATCHED THEN
      UPDATE SET GBN = C.GBN
 ;
 
MERGE INTO target_table_name
      USING (table|view|subquery) ON (join condition)
WHEN MATCHED THEN 
     UPDATE SET col1 = val1[, col2 = val2…]
WHEN NOT MATCHED THEN 
     INSERT(...) VALUES(...)
