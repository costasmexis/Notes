# Relational Databases (RDMS)
**Transactional or Online Transaction Processing (OLTP) System**
* Designed to store high volume day-to-day operational data
* Typically, relational, but can also be non-relational

**Analytical or Online Analytical Processing (OLAP) Systems**
* Optimized for conducting complex data analytics
* Include relational and non-relational databases, data warehouses, data lakes and big data stores

# SQL
__PostgreSQL__: Popular and in-demand version of SQL. (Free & Open Source)
- **PostgreSQL** - SQL Engine that stores data and reads queries and returns information.
- **PgAdmin** - Graphical User Interface for connecting with PostgreSQL. Lies on top of PostgreSQL.

## Database overview
* Databases are systems that allow users to store and organize data.
* They are useful when dealing with large amounts of data.

| Spreadsheet | Database |
|-------------|----------|
| Tabs | Tables |

# SQL Statements
### SELECT
```SQL
SELECT column_name FROM table_name;

SELECT DISTINCT column_name FROM table_name;
SELECT DISTINCT(column_name) FROM table_name;
```

### COUNT
Reutrn the number of input rows that match a specific condition of a query.

```SQL
SELECT COUNT column_name FROM table_name;

SELECT COUNT * FROM table_name;

SELECT COUNT(DISTINCT name) FROM table_name; 
```

### WHERE
The **WHERE** statement allows us to specify condition on columns for the rows to be returned.
The **WHERE** clause appears immediately after the FROM clause of the SELECT statement.

```SQL
# BASIC SYNTAX

SELECT column1, column2
FROM table_name
WHERE conditions;
```

TIP: `<> or != Not equal operator`

```SQL
Select name, choise From my_table 
Where name='David' AND choise='Red'
```

### ORDER BY
The **ORDER BY**  appears at the END of the query.

```SQL
# BASIC SYNTAX

SELECT column1, column2
FROM table_name
ORDER BY columns1 ASC/DESC;
```

- Use `ASC` to sort in ascending order
- Use `DESC` to sort in descending order
- If left blank, `ORDER BY` uses `ASC` by default

You can also `ORDER BY` multiple columns. This makes sense when one column has duplicate entries.

Let:
|Company|Name|Sales|
|--|--|--|
|Apple|Andrew|100|
|Google|David|500|
|Apple|Zach|300|
|Google|Claire|200|
|Xerox|Steven|100|

```SQL
SELECT company, name, sales FROM table_name
ORDER BY company, sales
```

Results in:
|Company|Name|Sales|
|--|--|--|
|Apple|Andrew|100|
|Apple|Zach|500|
|Google|Claire|300|
|Google|David|200|
|Xerox|Steven|100|

### LIMIT
- Allows us to limit the number of rows returned for a query
- Useful for not wanting to return every single row in a table, but only view the top few rows to get an idea of the table layout
- `LIMIT` also becomes useful in combination with `ORDER BY`
- `LIMIT` goes at the very end of a query request and is the last command to be executed

```SQL
e.x.

SELECT company, name, sales FROM table_name
WHERE sales != 100
ORDER BY company, sales DESC
LIMIT 5;
```

### BETWEEN
- Can be used to match a value against a range of values:
	- `value BETWEEN low AND high`
- Is the same as:
	- `value >= low AND value <= high`
- Can  also use `NOT BETWEEN`
- Can be used with dates

### IN
- In certain cases you want to check for multiple possible value options, for example, if a user's name shows up **IN** a list of known names
- We can use the **IN** operator to create a condition that checks to see if a value is included in a list of multiple options
```SQL
# Example

SELECT color FROM my_table
WHERE color IN ('red', 'blue', 'green')

SELECT color FROM my_table
WHERE color NOT IN ('red', 'blue', 'green')
```

### LIKE and ILIKE
`LIKE` is case-sensitive
`ILKE` is case-insensitive

What if we want to match against a general pattern in a string?
- All emails ending in '@gmail.com'
- All names that begin with an 'A'  (`... WHERE name LIKE 'A%'`)

The `LIKE` operator allows us to perform pattern matching against string data with the use of **wildcard** characers:
- Percent `%`
	- Matches any sequence of characters
- Underscore `_`
	- Matches any single character

Using the underscore allows us to replace just a single character
- Get all Mission Impossible films
	- `WHERE title LIKE "Mission Impossible _"`
- You can use multiple underscores
	- Image we had version string codes in the format  _'Version#A4'_
	- `WHERE value LIKE "Version#__"`
- We can also combine pattern matching operators to create more complex patterns

# GROUP BY Statements
`GROUP BY` will allow us to aggregate data and apply functions to better understand how data is distributed per category.

### Aggregate functions
The main idea behind an aggregate function is to take multiple inputs and return a single output.

Most Common Aggregate FunctionsQ
- `AVG()` - returns average value
- `COUNT()` - returns number of values
- `MAX()` - returns maximum value
- `MIN()` - returns minimum value
- `SUM()` - returns the sum of all values

Aggregate function calls happen only in the `SELECT` clause or the `HAVING` clause.

You can use `ROUND()` to specify precision after the decimal.

### GROUP BY
* __The `GROUP BY` clause must appear right after a `FROM` or `WHERE` statement.__
* __In the `SELECT` statement, columns must either have an aggregate function or be in the `GROUP BY` call.__
* __`WHERE` statements should not refer to the aggregation result. Use `HAVING` to filter on those results.__

|Category|Data Value|
|----|----|
|A|10|
|A|5|
|B|2|
|B|4|
|C|12|
|C|6|

```SQL
SELECT category_col, AVG(data_col)
FROM my_table
GROUP BY category_col;

# example

SELECT company, division, SUM(sales)
FROM finance_table
WHERE division IN ('marketing', 'transport')
GROUP BY company, division;
```
* __If you want to sort reults based on the aggregate, make sure to reference the entire function__
```SQL
SELECT company, SUM(sales)
FROM finance_table
GROUP BY company
ORDER BY SUM(sales)
LIMIT 5 DESC
```

### HAVING
- The `HAVING` clause allows us to filter __after__ an aggregation has already taken place

What if we want to filter based on SUM(sales) ? The SUM(sales) happens after the GROUP BY clause. 
```SQL
SELECT company, SUM(sales)
FROM finance_table
WHERE company != 'Google'
GROUP BY company
HAVING SUM(sales)>100   # CHECK THIS LINE
```

# JOINS
`JOINS` allow us to combine information from multiple tables! 
- INNER JOINS
- OUTER JOINS
- FULL JOINS
- UNIONS

### AS
The `AS` clause allows us to create an "alias" for a column or result.

```SQL
SELECT columns AS new_name
FROM my_table

ex.
SELECT SUM(amount) AS net_revenue
FROM payment;
```

 The `AS` operator gets executed at the very end of a query, meaning that we can not use the ALIAS inside a `WHERE` operator or a `HAVING` clause.

## INNER JOINS
The simplest JOIN type. 

- An INNER JOIN will result with the set of records that __match in both__ tables. 
- Again, an INNER JOIN is looking for matches that exist within both tables.
- INNER JOIN is symmetrical
```SQL
SELECT * FROM TableA
INNER JOIN TableB
ON TableA.col_match = TableB.col_match
```
```SQL
# Example:

SELECT * FROM Registrations
INNER JOIN Logins
  ON Registrations.name = Logins.name

# Define which columns to print. Specify from which table if the #columns exists in both columns

SELECT payment_id, payment.customer_id, first_name
FROM payment
INNER JOIN customer
ON payment.customer_id = customer.customer_id
```


## OUTTER JOINS
- There are few different types of OUTER JOINs
- They will allow us to specify how to deal with values only present in one of the tables being joined
- These are the more complex JOINs
