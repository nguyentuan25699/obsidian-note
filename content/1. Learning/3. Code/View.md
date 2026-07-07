## 1. View definition
- A view is a specific look on data from one or more tables. It can arrange data in some specific order, highlight or hide some data. A view consists of a stored query accessible as a virtual table composed of the result set of a query. Unlike ordinary tables a view does not form part of the physical schema. It is a dynamic, virtual table computed or collated from data in the database.
- A view is a pseudo table. It is a stored query which looks like a table. And it can be referenced like a table.
- Views can restrict users to specific rows or columns and thus enhance security. They can be used to join columns from multiple tables, so that they look like a single table. They can be used to provide aggregate information.

There are several restrictions that apply to views. Here are some of them:
- The SELECT statement cannot contain a subquery
- The SELECT statement cannot refer to system or user variables
- Any table or view referred to in the definition must exist
- A temporary VIEW cannot be created
- A VIEW cannot be associated with a trigger
___

## 2. Creating, modifying and dropping a View
- In the next example, we create a simple view. We use CREATE VIEW syntax to create a view. This is our data, upon which we create the view.

```sql
mysql> SELECT * FROM Cars;
+----+------------+--------+
| Id | Name       | Cost   |
+----+------------+--------+
| 1  | Audi       | 52642  |
| 2  | Mercedes   | 57127  |
| 3  | Skoda      | 9000   |
| 4  | Volvo      | 29000  |
| 5  | Bentley    | 350000 |
| 6  | Citroen    | 21000  |
| 7  | Hummer     | 41400  |
| 8  | Volkswagen | 21600  |
+----+------------+--------+
```

We create a view CheapCars. These are cars which cost under 25000.

```sql
CREATE VIEW CheapCars AS SELECT Name FROM Cars WHERE Cost<25000;
```
A view is a database object than can be queried. There are three cars which are considered to be cheap.

```sql 
mysql> SELECT * FROM CheapCars;
+------------+
| Name       |
+------------+
| Skoda      |
| Citroen    |
| Volkswagen |
+------------+
```

