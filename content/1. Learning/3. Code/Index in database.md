## 1. Basic Concepts of Indexing?
Database index is :
- A data structure that improves the speed of data retrieval operations on a database table at the cost of additional write and storage space to maintain the index data structure.
![[Pasted image 20260707214905.png]]

## 2. How it works?
  
How query work without index ?
- The database software would literally have to look at every single row until find the result. (Linear search)
![[Pasted image 20260707214951.png]]

When have index ?
- The whole point of having an index is to speed up search queries by essentially cutting down the number of records/rows in table that need to be examined by algorithm priority search.
![[Pasted image 20260707215035.png]]
___

## 3. Types of Indexes
![[Pasted image 20260707215123.png]]
___

## 4. Advantages and Disadvantages
![[Pasted image 20260707215257.png]]

- Table Users :
![[Pasted image 20260707215336.png]]
___

## 5. Syntax
- Create index
```sql
CREATE INDEX index_name ON table_name;
```
- Create single-column index
```sql
CREATE INDEX index_name ON table_name (column_name);
```
- Create unique index
```sql
CREATE UNIQUE INDEX index_name ON table_name (column_name);
```
- Create composite index
```sql
CREATE INDEX index_name ON table_name (column_name_1,column_name_2);
```
- Drop index
```sql
DROP INDEX index_name;
```
