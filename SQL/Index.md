## INDEX
An index is a database object that improves the speed of data retrieval operations on a table. It is created on one or more columns in a table to make searching faster. However, indexes can slow down write operations (INSERT, UPDATE, DELETE) since the index must be updated when the data changes.
-   **Unique Index**: Ensures that all values in a column are distinct.
-   **Non-Unique Index**: Allows duplicate values in the indexed column.

**SYNTAX**
```sql
CREATE INDEX idx_employee_name ON employees(name);
```
### Types of Indexing in SQL
1.  Clustered Index:
-   A clustered index determines the physical order of data in a table.
-   There can be only **one clustered index per table** because the data rows themselves can be sorted in only one order.
-   By default, primary key creates a clustered index (unless specified otherwise).
-   Best for range queries and sorting.
    #### 🧩 Example
    ```sql
    CREATE CLUSTERED INDEX idx_EmployeeId ON Employees(EmployeeId);
    ```
2.  Non-Clustered Index:
-   A non-clustered index is a separate structure that stores a sorted list of values along with pointers to the corresponding rows in the table.
-   A table can have multiple non-clustered indexes.
-   Great for frequent search/filtering on non-key columns.
-   Can be covering index if it includes extra columns.
    #### 🧩 Example
    ```sql
    CREATE INDEX idx_LastName ON Employees(LastName);
    ```
3.  Unique Index:
-   A unique index ensures that the values in the indexed column(s) are unique across the table.
-   It helps in enforcing uniqueness constraints.
-   Can be clustered or non-clustered.
    #### 🧩 Example
    ```sql
    CREATE UNIQUE INDEX idx_UniqueEmail ON Employees(Email);
    ```
4.  Composite Index
-   A composite index is an index on multiple columns of a table. It is useful for queries that filter on multiple columns.
    #### 🧩 Example
    ```sql
    CREATE INDEX idx_FirstLastName ON Employees(FirstName, LastName);
    ```
5.  Full-Text Index:
-   A full-text index allows for complex queries on textual data, such as searching for words or phrases within text columns.
    #### 🧩 Example
    ```sql
    CREATE FULLTEXT INDEX ON Documents(Content) KEY INDEX PK_Documents;
    ```
6.  Filtered Index:
-   A filtered index is an optimized non-clustered index that includes only a subset of rows, based on a filter condition.
    #### 🧩 Example
    ```sql
    CREATE INDEX idx_ActiveEmployees ON Employees(Status) WHERE Status = 'Active';
    ```
#### which one is faster Cluster Index or Non Cluster Index?
**Answer:**
“Clustered indexes are generally faster for range queries and sorting, since the data is physically ordered. Non-clustered indexes are faster for point lookups and when designed as covering indexes, since they can serve queries without going back to the base table. So the speed depends on the query pattern — neither is always faster.”
-   👉 If you need range scans or sorting → Clustered is faster.
-   👉 If you need quick lookups on specific columns → Non-Clustered is faster.