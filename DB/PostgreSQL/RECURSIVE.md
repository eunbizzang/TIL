
PostgreSQL RECURSIVE Query
```
WITH RECURSIVE subordinates AS (
	SELECT
		menu_id,
    menu_parent_id,
    menu_nm
	FROM
		menu_tbl
	WHERE
		menu_parent_id = ''
	UNION
		SELECT
			e.menu_id,
      e.menu_parent_id,
      e.menu_nm
		FROM
			menu_tbl e
		INNER JOIN subordinates s ON s.menu_id = e.menu_parent_id
) SELECT
	*
FROM
	subordinates;
```
