https://www.postgresqltutorial.com/

<h2>I/ SELECT: Query</h2>

```
// Query a column from table database
SELECT coulmn FROM table;

// Query two columns from table database
SELECT coulmn1, column2, column3 FROM table;

// Query all records from table database
SELECT \* FROM table;

// Query column1 and column2 and merge them into a single column with an expression " " between them from table database
SELECT column1 || " " || column2 FROM table;
```

<h2>II/ Column aliases: Better column name for Output</h2>

```
// Query column1 and re-name the name of the column1 to alias for the output from table database
SELECT column1 AS alias_name FROM table;
// Query column1 and re-name the name of the column1 to the alias ( with space in it ) from the table database
SELECT column1 "alias name with space" FROM table;
```

<h2>III/ ORDER BY: Sorting column</h2>

```
// Query column1 from table database and sort them based on pla pla
SELECT column1 FROM table ORDER BY sort_expression1 [ASC, DESC] [NULL FIRST | NULL LAST], sort_expression2 [ASC, DESC] [NULL FIRST | NULL LAST];
```

<h2>IV/ SELECT DISTINCT: Removing duplicated values of row</h2>

```
// Query column from table database and remove duplicated values of row record then sort them by that column
SELECT DISTINCT column FROM table ORDER BY column;
```

<h2>V/ WHERE: filter rows records</h2>

| Operation | Meaning                                           |
| --------- | ------------------------------------------------- |
| =         | EQUAL                                             |
| >         | GREATER THAN                                      |
| <         | LESS THAN                                         |
| >=        | GREATER OR EQUAL THAN                             |
| <=        | LESSER OR EQUAL THAN                              |
| !=        | NOT EQUAL                                         |
| AND       | AND                                               |
| OR        | OR                                                |
| IN        | RETURN TRUE IF A VALUE MATCHES VALUES IN THE LIST |
| BETWEEN   | RETURN TRUE IF A VALUE BETWEEN RANGE OF VALUES    |
| LIKE      | RETURN TRUE IF A VALUE MATCHES A PATTERN          |
| IS NULL   | RETURN TRUE IF VALUE IS NULL                      |
| NOT       | NEGATE THE RESULT OF OTHER OPERATORS              |

```
# Basic example :
SELECT last_name, first_name FROM table WHERE first_name="Tri";

# AND example :
SELECT first_name, last_name FROM table WHERE first_name="Tri" AND last_name="Tran";

# OR example :
SELECT first_name, last_name FROM table WHERE first_name="Tri" OR last_name="Tran";

# IN example :
SELECT first_name, last_name FROM table WHERE first_name IN ("Tri", "Thao", "Trang");

# LIKE example :
# 'foo' LIKE 'foo' true
# 'foo' LIKE 'f%' true
# 'foo' LIKE '_0_' true
# 'foo' LIKE 'f_' false
# LIKE | NOT LIKE | ILIKE (match values case-insenitively)
SELECT first_name, last_name FROM table WHERE first_name LIKE "Tr%";

# BETWEEN example :
SELECT first_name, LENGTH(first_name) length_name FROM table WHERE first_name LIKE "Tr%" AND LENGTH(first_name) BETWEEN 3 AND 5 ORDER BY length_name;

# NOT EQUAL example :
SELECT first_name FROM table WHERE first_name != "Tri";

# IS NULL :
SELECT first_name, phone FROM table WHERE first_name IS NULL;
```

<h2>VI/ LIMIT: limit number of rows you get, often time you will use LIMIT to get the top 10 highest items after sorting</h2>
```
SELECT column FROM table SORT BY sort_expression LIMIT row_count
```

<h2>VII/ JOIN: Query data from one or more tables</h2>

1. INNER JOIN

![InnerJoin](/POSTgreSQL/InnerJoin.PNG)

```
# Query all payments from a customer with id="123" sort by payment_date example :

SELECT
    customer_id,
    first_name,
    last_name,
    payment_date
FROM
    customer
INNER JOIN
    payment
ON
    payment.customer_id = customer.customer_id
WHERE
    customer_id="123"
ORDER BY
    payment_date;

# Query the customer based on the customer_id from a spicific payment example :

SELECT
    customer_id,
    payment_id,
    first_name,
    last_name,
    email,
FROM
    payment
INNER JOIN
    customer
ON
    payment.customer_id = customer.customer_id
WHERE
    payment_id="123"
```

<h2>VIII/ GROUP BY: Divide rows into groups and apply an aggerate function to each group</h2>

- POSTgreSQL evaluates GROUP_BY in the following orders : FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> DISTINCT -> ORDER BY -> LIMIT

```
# Query customer_id of payments FROM payment database and group them customer_id
# Essentially checking if a customer has a payment or not, if yes, print it out as result

SELECT customer_id FROM payment GROUP BY customer_id;

# Using GROUP BY with aggregation function
# Checking the total amount of all payments belong to a customer

SELECT customer_id, SUM(amount) FROM table GROUP BY customer_id;

# Using GROUP BY and INNER JOIN together
# Checking and sorting the top 10 users with higher total amount of payments

SELECT
    first_name || " " || last_name full_name
    SUM(amount) amount
FROM
    payment
INNER JOIN
    customer USING (customer_id)
GROUP BY
    full_name
ORDER BY
    amount
LIMIT 10;

# Using GROUP BY and DATE arregation function
# Calculate the date and the amount then sort them by payment_date and return the results

SELECT DATE(payment_date) payment_date, SUM(amount) amount FROM payment GROUP BY payment_date ORDER BY payment_date;
```

<h2>IX/ HAVING: Apply condition for group of rows</h2>

```
# Grouping by customer_id and only get the result that total of amount is more than 200 for one customer
SELECT customer_id, SUM(amount) FROM payment GROUP BY customer_id HAVING SUM(amount) > 200;
```
