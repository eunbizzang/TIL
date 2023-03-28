
```
UPDATE Table_Name
SET Column_Name = REPLACE(Column_Name, 'delete data', '');
```


```
UPDATE Table_Name 
  SET Column_Name = replace(Column_Name, '&reg', '&amp;reg')
   WHERE  Column_Name LIKE '%&reg%';
```