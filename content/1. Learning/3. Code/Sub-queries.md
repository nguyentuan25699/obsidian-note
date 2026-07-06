## 1. What is subqueries
- A subquery is a query in a query. It is also called an inner query or a nested query. A subquery can be used anywhere an expression is allowed. It is a query expression enclosed in parentheses. Subqueries can be used with SELECT, INSERT, UPDATE, or DELETE statements.
- There is more than one way to execute an SQL task. Many subqueries can be replaced by SQL joins. SQL joins are usually faster.
- We recapitulate what we have in the Customers and Reservations tables. Subqueries are often performed on tables, which have some relationship.

```sql
SELECT * FROM Customers; 
+------------+-------------+
| CustomerId | Name        |
+------------+-------------+
| 1          | Tom Willis  |
| 2          | Terry Neils |
| 3          | Cindy Mason |
| 4          | Paul Novak  |
| 5          | Jack Fonda  |
+------------+-------------+
5 rows in set (0.00 sec)

SELECT * FROM Reservations;
+----+------------+------------+
| Id | CustomerId | Day        |
+----+------------+------------+
| 1  | 1          | 2009-11-22 |
| 2  | 2          | 2009-11-28 |
| 3  | 2          | 2009-11-29 |
| 4  | 1          | 2009-11-29 |
| 5  | 3          | 2009-12-02 |
+----+------------+------------+
5 rows in set (0.00 sec)
```

