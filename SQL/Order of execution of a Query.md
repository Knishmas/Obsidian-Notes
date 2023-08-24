Source: https://sqlbolt.com/lesson/select_queries_order_of_execution


# A Complete SELECT query

```sql 
SELECT DISTINCT column, AGG_FUNC(_column_or_expression_), … FROM mytable 
	JOIN another_table
		ON mytable.column = another_table.column 
	WHERE _constraint_expression_ 
	GROUP BY column 
	HAVING _constraint_expression_ 
	ORDER BY _column_ ASC/DESC 
	LIMIT _count_ OFFSET _COUNT_;
```