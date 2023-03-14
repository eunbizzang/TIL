https://gent.tistory.com/406


인라인뷰(서브쿼리)
```

MERGE 
 INTO emp a
USING (SELECT aa.empno
            , aa.job
            , aa.deptno
         FROM emp aa
            , dept bb
        WHERE aa.empno = 7788
          AND aa.deptno = bb.deptno) b
   ON (a.empno = b.empno)
 WHEN MATCHED THEN
      UPDATE
         SET a.job = b.job
           , a.deptno = b.deptno
 WHEN NOT MATCHED THEN
      INSERT (a.empno, a.job, a.deptno)
      VALUES (b.empno, b.job, b.deptno);
```
