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

## SQL Statements
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







