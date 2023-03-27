http://gurubee.net/article/66200

```
WITH t AS
(
SELECT 1 no, '1234' v FROM dual
UNION ALL SELECT 2, 'abcd' FROM dual
UNION ALL SELECT 3, '가나다' FROM dual
UNION ALL SELECT 4, '1가ab' FROM dual
UNION ALL SELECT 5, 'gurubee.net' FROM dual
)
SELECT no, v
     , CASE WHEN REGEXP_LIKE(v, '[0-9]') THEN 1 END 숫자포함
     , CASE WHEN REGEXP_LIKE(v, '[A-Za-z]') THEN 1 END 영문포함
     , CASE WHEN REGEXP_LIKE(v, '[가-힝]') THEN 1 END 한글포함
     , CASE WHEN REGEXP_REPLACE(v, '[[:alnum:]]') IS NOT NULL THEN 1 END 특수문자포함
  FROM t
;
```