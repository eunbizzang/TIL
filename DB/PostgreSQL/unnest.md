https://www.postgresql.org/docs/9.2/functions-array.html

- unnest(anyarray)	setof anyelement	expand an array to a set of rows	
```
unnest(ARRAY[1,2])	

1
2
(2 rows)
```

- ROWNUM()
```
SELECT ROW_NUMBER() OVER() AS ROWNUM, *
FROM DEPT;
```

- ROWNUM() + unnest
```
select ROW_NUMBER() OVER() as array_sequence, array_id
		from (
			select unnest(string_to_array(array_list, ',')) as array_id
			from table
			) as alias_name;


---- RESULT ----
array_id(ARRAY[A,B,C,D])	

array_sequence  array_id
1                  A
2                  B
3                  C
4                  D
(4 rows)
```
