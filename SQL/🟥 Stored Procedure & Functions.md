## <span style="background-color:#ff4d4d; color:white; padding:2px 6px; border-radius:4px;">High</span> STORED PROCEDURE 
Stored procedures in Oracle are precompiled SQL code that is stored in the database and can be executed on demand. They are used to encapsulate business logic and improve performance by reducing the amount of data transferred between the application and the database.

### Stored Procedure vs Functions
Feature | Function | Stored Procedure|
|-----------|-------------|-----------|
**Definition** | A function is a named block of code that can accept parameters, perform operations, and return a value. | A stored procedure is a set of SQL statements that can perform operations on the database (e.g., insert, update, delete) and can accept input parameters, but unlike functions, it doesn’t necessarily return a value.
**Example** | `CREATE FUNCTION GetEmployeeSalary (@EmpID INT) RETURNS DECIMAL AS BEGIN RETURN (SELECT Salary FROM Employees WHERE EmployeeID = @EmpID); END;` | `CREATE PROCEDURE UpdateEmployeeSalary (@EmpID INT, @NewSalary DECIMAL) AS BEGIN  UPDATE Employees SET Salary = @NewSalary WHERE EmployeeID = @EmpID; END;`
**Key Point** |  A function can be used inside queries (e.g., SELECT statements). | A stored procedure can't be used directly inside queries. |
**Return Value** | A function returns a value (e.g., scalar value or table) | A stored procedure does not (though it can return result sets). |
**Usage** | Functions can be used in queries | stored procedures are called explicitly and usually involve a series of actions. |
**Try-Catch** | Functions cannot be directly used in Try-Catch Block | Stored procedures can be used in Try-Catch Block |
**Execution Plan Reusebility** | They do not maintain their own execution plan and are recompiled as part of the parent query. <br> Functions (scalar or table-valued) are treated as part of the query where they are invoked. | The SQL Server compiles and caches the execution plan for stored procedures upon their first execution. <br> This means that for subsequent calls, the precompiled execution plan is reused, reducing overhead.
**Performance** | Slower for Large Datasets, especially scaler functions | Faster due to precompiled execution plan |
**DML Operations** | Does not supports DML Operations | Supports DML Operations `DELETE, INSERT, UPDATE` |
**Caching** | No separate execution plan is cached | Execution plan is cached | 
#### Stored procedures are faster than functions primarily because of execution plan caching, batch processing, and reduced context switching. While both have their specific use cases, stored procedures are ideal for performance-critical and complex operations, whereas functions are better suited for simpler, reusable logic.
#### If I give you one SP to optimize what would be your thought process?
**Answer:**
“My thought process starts with understanding the stored procedure’s purpose and current performance. Then I run it with execution plans and statistics `(SET STATISTICS IO ON, SET STATISTICS TIME ON)` to identify bottlenecks (e.g., heavy scans, costly sorts, nested loops). I analyze for table scans, missing indexes, non-SARGable conditions, or inefficient joins. Next, I apply optimizations like adding indexes, rewriting queries for better SARGability, avoiding `SELECT *`, reducing cursors, checking filters (Sargable predicates (e.g., WHERE YEAR(date) = 2023 ❌ → WHERE date >= '2023-01-01' ✅)) and checking for parameter sniffing. After changes, I retest performance with real data and ensure results are correct. Finally, I suggest long-term improvements like monitoring, caching, and schema adjustments.”