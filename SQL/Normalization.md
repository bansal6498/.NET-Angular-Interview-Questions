## Normalization
Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity. It involves dividing large tables into smaller ones and defining relationships between them.
There are several normal forms (1NF, 2NF, 3NF, BCNF, etc.), with each having a set of rules to achieve higher levels of normalization.
-   **1NF** (First Normal Form): Ensures that the table contains only atomic (indivisible) values and each record is unique.
-   **2NF** (Second Normal Form): Achieved when a table is in 1NF and all non-key attributes are fully dependent on the primary key.
-   **3NF** (Third Normal Form): Achieved when a table is in 2NF and all attributes are functionally dependent only on the primary key.
#### What is normalization in SQL, and why is it important?
**Answer:**
Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity. It involves dividing a database into two or more tables and defining relationships between them. The primary goals are to eliminate duplicate data, ensure data dependencies make sense, and simplify the schema.
#### Explain the different types of normal forms in database normalization.
**Answer:**
-   **First Normal Form (1NF)**: Ensures that the table has a primary key and each column contains atomic (indivisible) values.
-   **Second Normal Form (2NF)**: Meets all the requirements of 1NF and ensures that all non-key attributes are fully functional dependent on the primary key.
-   **Third Normal Form (3NF)**: Meets all the requirements of 2NF and ensures that all non-key attributes are not transitive dependent on the primary key (i.e., non-key attributes do not depend on other non-key attributes).