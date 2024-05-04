# Description 
Here are some basic and advance sql server concepts and questions.

# Table of contents
1. [Basic Sql Server concepts](#Basic-sqlserver)
2. [Advance Sql Server with examples](#Advance-sqlserver)
3. [Advance Sql Server concepts](#Advance-sqlserver-concepts)



# Basic Sql Server concepts<a id="Basic-sqlserver"></a>
1. **What is SQL Server, and what are its key components?**

   - **Answer:** 
     - SQL Server is a relational database management system (RDBMS) developed by Microsoft.
     - Its key components include the Database Engine, which manages data storage, processing, and security; SQL Server Management Studio (SSMS), a graphical tool for managing databases; Integration Services (SSIS) for ETL (Extract, Transform, Load) operations; Analysis Services (SSAS) for data analysis and OLAP (Online Analytical Processing); and Reporting Services (SSRS) for creating and delivering reports.

2. **What is a primary key, and why is it important in a SQL Server database?**

   - **Answer:** 
     - A primary key is a column or a set of columns that uniquely identify each row in a table.
     - It ensures data integrity by enforcing entity integrity constraints, preventing duplicate records, and providing a reference for relationships between tables.

3. **What is a foreign key, and how is it used in SQL Server?**

   - **Answer:** 
     - A foreign key is a column or a set of columns that establishes a relationship between two tables in a SQL Server database.
     - It enforces referential integrity by requiring that the values in the foreign key column(s) match the values in the corresponding primary key column(s) of another table.

4. **What is the difference between a clustered and a non-clustered index in SQL Server?**

   - **Answer:** 
     - A clustered index determines the physical order of data rows in a table and is stored in the same order as the data.
     - A non-clustered index creates a separate structure that points to the data rows in a table and does not affect the physical order of data.
     - Each table can have only one clustered index but multiple non-clustered indexes.

5. **Explain the purpose of the SQL SELECT statement.**

   - **Answer:** 
     - The SELECT statement retrieves data from one or more tables in a SQL Server database.
     - It allows you to specify the columns to retrieve, filter rows using WHERE clause conditions, sort the result set using ORDER BY clause, and perform aggregate functions such as SUM, COUNT, AVG, etc.

6. **What is the difference between the WHERE and HAVING clauses in SQL Server?**

   - **Answer:** 
     - The WHERE clause is used to filter rows from the result set based on specified conditions before grouping and aggregation.
     - The HAVING clause is used to filter grouped rows from the result set based on specified conditions after grouping and aggregation.

7. **How do you perform a JOIN operation in SQL Server?**

   - **Answer:** 
     - JOIN operation combines rows from two or more tables based on a related column between them.
     - Common types of JOIN include INNER JOIN (returns rows that have matching values in both tables), LEFT JOIN (returns all rows from the left table and matching rows from the right table), and RIGHT JOIN (returns all rows from the right table and matching rows from the left table).

8. **What is the purpose of the SQL GROUP BY clause?**

   - **Answer:** 
     - The GROUP BY clause is used to group rows from a result set based on one or more columns.
     - It is typically used with aggregate functions such as SUM, COUNT, AVG, etc., to perform calculations on groups of rows.

9. **What is a SQL Server stored procedure, and how do you create one?**

   - **Answer:** 
     - A stored procedure is a precompiled and reusable SQL code block stored in the database.
     - It can accept input parameters, perform operations such as querying, updating, or deleting data, and return results to the caller.
     - You can create a stored procedure using the CREATE PROCEDURE statement in SQL Server Management Studio (SSMS) or any SQL client tool.

10. **Explain the purpose of SQL Server transactions and how they ensure data integrity.**

    - **Answer:** 
      - A transaction is a sequence of one or more SQL statements that are executed as a single unit of work.
      - It ensures data integrity by providing the ACID properties (Atomicity, Consistency, Isolation, Durability) to database operations.
      - Transactions can be started with the BEGIN TRANSACTION statement, committed with the COMMIT statement if successful, or rolled back with the ROLLBACK statement if an error occurs.


# Advance Sql Server concepts<a id="Advance-sqlserver"></a>
1. **Write a SQL query to find the second highest salary from the Employee table.**

   - **Answer:** 
     ```sql
     SELECT MAX(Salary) AS SecondHighestSalary
     FROM Employee
     WHERE Salary < (SELECT MAX(Salary) FROM Employee);
     ```

2. **Explain the difference between INNER JOIN, LEFT JOIN, and RIGHT JOIN with examples.**

   - **Answer:** 
     - INNER JOIN: Returns rows that have matching values in both tables.
       ```sql
       SELECT Orders.OrderID, Customers.CustomerName
       FROM Orders
       INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
       ```
     - LEFT JOIN: Returns all rows from the left table and matching rows from the right table.
       ```sql
       SELECT Orders.OrderID, Customers.CustomerName
       FROM Orders
       LEFT JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
       ```
     - RIGHT JOIN: Returns all rows from the right table and matching rows from the left table.
       ```sql
       SELECT Orders.OrderID, Customers.CustomerName
       FROM Orders
       RIGHT JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
       ```

3. **Write a SQL query to calculate the running total of a column in a table.**

   - **Answer:** 
     ```sql
     SELECT OrderDate, Amount,
            SUM(Amount) OVER (ORDER BY OrderDate) AS RunningTotal
     FROM Orders;
     ```

4. **Explain the purpose of Common Table Expressions (CTEs) and provide an example.**

   - **Answer:** 
     - Common Table Expressions (CTEs) provide a way to define temporary result sets that can be referenced within a SQL statement.
     - They improve readability, maintainability, and reusability of complex queries.
     - Example:
       ```sql
       WITH CTE AS (
           SELECT EmployeeID, FirstName, LastName, ROW_NUMBER() OVER (ORDER BY LastName) AS RowNum
           FROM Employees
       )
       SELECT EmployeeID, FirstName, LastName
       FROM CTE
       WHERE RowNum <= 10;
       ```

5. **Write a SQL query to find the nth highest salary from the Employee table.**

   - **Answer:** 
     ```sql
     SELECT DISTINCT Salary
     FROM Employee E1
     WHERE n = (
         SELECT COUNT(DISTINCT Salary)
         FROM Employee E2
         WHERE E1.Salary <= E2.Salary
     );
     ```

6. **Explain the difference between UNION and UNION ALL with examples.**

   - **Answer:** 
     - UNION: Combines the result sets of two or more SELECT statements and removes duplicate rows.
       ```sql
       SELECT City FROM Customers
       UNION
       SELECT City FROM Suppliers;
       ```
     - UNION ALL: Combines the result sets of two or more SELECT statements, including duplicate rows.
       ```sql
       SELECT City FROM Customers
       UNION ALL
       SELECT City FROM Suppliers;
       ```

7. **Write a SQL query to find the longest consecutive sequence of consecutive numbers in a table.**

   - **Answer:** 
     ```sql
     SELECT MIN(num) AS StartRange, MAX(num) AS EndRange, COUNT(*) AS ConsecutiveCount
     FROM (
         SELECT num, ROW_NUMBER() OVER (ORDER BY num) - ROW_NUMBER() OVER (PARTITION BY num ORDER BY num) AS grp
         FROM NumbersTable
     ) AS T
     GROUP BY grp
     ORDER BY ConsecutiveCount DESC
     LIMIT 1;
     ```

8. **Explain the purpose of the ROW_NUMBER() function in SQL Server and provide an example.**

   - **Answer:** 
     - The ROW_NUMBER() function assigns a unique sequential integer to each row within a partition of a result set.
     - It is often used for pagination, ranking, and partitioning data.
     - Example:
       ```sql
       SELECT ProductID, ProductName, UnitPrice,
              ROW_NUMBER() OVER (PARTITION BY CategoryID ORDER BY UnitPrice DESC) AS Rank
       FROM Products;
       ```

9. **Write a SQL query to find the top N records from a table, skipping the first M records.**

   - **Answer:** 
     ```sql
     SELECT *
     FROM (
         SELECT *, ROW_NUMBER() OVER (ORDER BY ID) AS RowNum
         FROM Table
     ) AS T
     WHERE RowNum > M
     AND RowNum <= M + N;
     ```

10. **Explain the purpose of the PIVOT and UNPIVOT operators in SQL Server and provide an example for each.**

    - **Answer:** 
      - PIVOT: Rotates a table-valued expression by turning the unique values from one column into multiple columns in the output.
        ```sql
        SELECT *
        FROM (
            SELECT ProductID, CategoryID, UnitPrice
            FROM Products
        ) AS SourceTable
        PIVOT (
            AVG(UnitPrice)
            FOR CategoryID IN ([1], [2], [3], [4])
        ) AS PivotTable;
        ```
      - UNPIVOT: Converts column-based data into row-based data by rotating columns into rows.
        ```sql
        SELECT ProductID, CategoryID, UnitPrice
        FROM (
            SELECT [1] AS Category1, [2] AS Category2, [3] AS Category3, [4] AS Category4
            FROM PivotTable


        ) AS SourceTable
        UNPIVOT (
            UnitPrice FOR CategoryID IN (Category1, Category2, Category3, Category4)
        ) AS UnpivotTable;
        ```

# Advance Sql Server concepts<a id="Advance-sqlserver-concepts"></a>
1. **Atomicity, Consistency, Isolation, Durability (ACID) Principle:**
   - ACID is a set of properties that ensures reliability and consistency in database transactions.
   - Atomicity: Ensures that a transaction is treated as a single unit of work, either all of its operations are completed successfully or none of them are.
   - Consistency: Ensures that a transaction takes the database from one consistent state to another, maintaining all data integrity constraints.
   - Isolation: Ensures that the concurrent execution of transactions produces a result that is equivalent to a serial execution of transactions, preventing interference between transactions.
   - Durability: Ensures that the changes made by committed transactions are permanent and survive system failures, crashes, or restarts.

2. **Normalization:**
   - Normalization is the process of organizing data in a database to reduce redundancy and dependency.
   - It involves dividing a database into multiple tables and defining relationships between them to minimize duplication of data and ensure data integrity.
   - Normalization eliminates anomalies such as insertion, update, and deletion anomalies, which can occur when data is stored redundantly or inappropriately.

3. **Database Indexing:**
   - Indexing is a database optimization technique used to improve the speed of data retrieval operations, such as SELECT queries.
   - It involves creating data structures (indexes) that store keys extracted from the columns of a table, along with pointers to the corresponding rows.
   - Indexes allow the database engine to quickly locate and retrieve data based on search criteria specified in queries, reducing the need for full-table scans.

4. **Transaction Isolation Levels:**
   - Transaction isolation levels define the degree of isolation between concurrent transactions in a database.
   - Common isolation levels include READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, and SERIALIZABLE.
   - Each isolation level provides a different level of consistency and concurrency control, balancing performance and data integrity requirements.

5. **Data Warehousing and OLAP:**
   - Data warehousing is the process of collecting, storing, and managing large volumes of structured and unstructured data from various sources for analysis and reporting.
   - Online Analytical Processing (OLAP) is a technology used for performing complex analytical queries and generating reports from multidimensional data stored in data warehouses.
   - OLAP databases are optimized for read-heavy workloads and support features such as multidimensional data models, advanced querying capabilities, and aggregation functions.

6. **Partitioning:**
   - Partitioning is a database optimization technique used to divide large tables or indexes into smaller, more manageable partitions.
   - It improves performance, manageability, and availability by distributing data across multiple storage devices or filegroups.
   - Partitioning can be based on ranges of values, list of values, or hash functions, allowing for efficient data retrieval and maintenance operations.

7. **Database Sharding:**
   - Sharding is a horizontal scaling technique used to distribute data across multiple independent databases (shards) to improve scalability and performance.
   - Each shard contains a subset of data and can handle a portion of the overall workload, reducing the load on individual databases and improving throughput.
   - Sharding requires careful planning and implementation to ensure data consistency, availability, and reliability across shards.
