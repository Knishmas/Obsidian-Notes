Source: https://sqlbolt.com/lesson/select_queries_order_of_execution


# A Complete SELECT query

**General template**
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

*Example*

# Inserting rows 
**General template**
```sql
Insert statement with values for all columns

INSERT INTO mytable 
VALUES (value_or_expr, another_value_or_expr, …), (value_or_expr_2, another_value_or_expr_2, …), …;
```

*Example*
```sql
INSERT INTO movies 
VALUES (4, "Toy Story 4", "El Directore", 2015, 90);
```

# Updating rows 
**General template**
```sql 
UPDATE mytable 
SET column = value_or_expr,
	other_column = another_value_or_expr, … 
WHERE condition;
```

*Example*
```sql
UPDATE movies 
SET title = "Toy Story 3", 
    director = "Lee Unkrich"
WHERE id = 11;
```

# Deleting rows 
**General template**
```sql
CREATE TABLE IF NOT EXISTS mytable ( 
	column _DataType_ _TableConstraint_ DEFAULT 
	_default_value_, another_column _DataType_  _TableConstraint_ DEFAULT _default_value_, … );
```

*Example*
```sql
DELETE from movies
WHERE year < 2005;
```

# Creating a table
**General template**
```sql 
CREATE TABLE IF NOT EXISTS mytable ( 
	column _DataType_ _TableConstraint_ DEFAULT 
	_default_value_, another_column _DataType_ 
	_TableConstraint_ DEFAULT _default_value_,
	 … 
	 );
	```

*Example
```sql
CREATE TABLE IF NOT EXISTS database(
name STRING, 
version FLOAT, 
download_count INTEGER
);
```

# Altering Tables
**General template**
```sql 
ALTER TABLE mytable 
ADD column _DataType_ _OptionalTableConstraint_ 
	DEFAULT default_value;
```

