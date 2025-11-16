# Complete DBMS Interview Notes

## Table of Contents

1. [Introduction to Databases](#1-introduction-to-databases)
2. [Relational Model](#2-relational-model)
3. [ER Model (Entity-Relationship Model)](#3-er-model-entity-relationship-model)
4. [Normalization (Data Organization)](#4-normalization-data-organization)
5. [SQL Basics (Foundation)](#5-sql-basics-foundation)
6. [Querying Data](#6-querying-data)
7. [Aggregate Functions](#7-aggregate-functions)
8. [Joins](#8-joins)
9. [Subqueries](#9-subqueries)
10. [Set Operations](#10-set-operations)
11. [Functions in SQL](#11-functions-in-sql)

---

## 1. Introduction to Databases

### Database Management System (DBMS)? What are its types, advantages, and applications?

A **Database Management System (DBMS)** is software used to efficiently manage and organize databases. It provides an interface for storing, retrieving, updating, and managing data while ensuring **data integrity**, **security**, and **concurrency control**. Examples include **MySQL**, **PostgreSQL**, **Oracle**, and **SQL Server**.

#### Types of DBMS:
1. **Hierarchical DBMS** – Organizes data in a tree-like structure with parent-child relationships.  
   *Example:* IBM IMS  
2. **Network DBMS** – Represents data as a graph with many-to-many relationships.  
   *Example:* Integrated Data Store (IDS)  
3. **Relational DBMS (RDBMS)** – Stores data in tables (relations) and manages it using SQL.  
   *Example:* MySQL, PostgreSQL  
4. **Object-Oriented DBMS** – Stores data as objects, similar to object-oriented programming.  
   *Example:* ObjectDB  

#### Advantages of DBMS:
- **Data Integrity:** Maintains accuracy and consistency of data.  
- **Data Security:** Provides controlled access via user permissions.  
- **Efficient Retrieval:** Uses indexing and query optimization for faster results.  
- **Reduced Redundancy:** Minimizes duplicate data through normalization.  
- **Backup & Recovery:** Supports automatic backup and restoration.  
- **Concurrent Access:** Enables multiple users to work simultaneously without conflicts.  

#### Applications of DBMS:
- **Banking:** Account management, transaction processing.  
- **E-commerce:** Product catalogs, order tracking, customer data.  
- **Healthcare:** Patient records, diagnosis history.  
- **Education:** Student grades, schedules, course management.  
- **Social Media:** User profiles, interactions, content storage.  
- **Data Science:** Storing and processing large datasets for analytics and predictions.  

**Illustration:**  
![Database Applications](https://media.geeksforgeeks.org/wp-content/uploads/20250729183922080793/Database-Applications.webp)

---

### What are the problems with traditional file-based systems?

Before the introduction of modern DBMS, data was stored and managed using basic file systems on hard drives. Although these systems allowed storing, retrieving, and updating files, they had several drawbacks:

- **Data Redundancy:** Duplicate entries often existed across multiple files.  
- **Data Inconsistency:** Conflicting or outdated information could occur due to redundant storage.  
- **Difficult Data Access:** Manual searching was time-consuming and inefficient.  
- **Poor Security:** No built-in access control to restrict unauthorized access.  
- **Single-User Limitation:** No support for multi-user collaboration.  
- **No Backup & Recovery:** Data loss was often permanent without recovery mechanisms.  

---

### What is the difference between DBMS and RDBMS?

- **DBMS (Database Management System):**  
  A software system that enables users to create, store, modify, and delete data. It does **not** require a relational structure for organizing data.  
  *Examples:* Microsoft Access, XML databases.

- **RDBMS (Relational Database Management System):**  
  A type of DBMS that stores data in structured **tables (relations)** and supports relational operations like **joins**. It enforces **data integrity** using primary keys and foreign keys, and supports SQL for querying.  
  *Examples:* MySQL, Oracle, SQL Server.

---

### What is the difference between File System and DBMS?

| Aspect                | File System | DBMS |
|-----------------------|-------------|------|
| **Data Storage**      | Stores data in separate files without structured relationships. | Stores data in a structured format (tables, objects) with relationships. |
| **Data Redundancy**   | High redundancy due to duplicate records in multiple files. | Redundancy minimized through normalization. |
| **Data Consistency**  | Inconsistencies common due to lack of centralized control. | Maintains consistency via integrity constraints. |
| **Data Access**       | Manual searching; slow for large datasets. | Uses query languages (e.g., SQL) for efficient retrieval. |
| **Security**          | Limited or no built-in access control. | Role-based permissions and authentication mechanisms. |
| **Multi-user Support**| Typically single-user; difficult for concurrent access. | Supports concurrent multi-user operations with concurrency control. |
| **Backup & Recovery** | No automatic backup/recovery; data loss may be permanent. | Provides built-in backup and recovery mechanisms. |
| **Data Integrity**    | No enforcement of data validation rules. | Enforces integrity via constraints (primary key, foreign key, etc.). |

---

### What are the different types of DBMS architecture?

A **DBMS architecture** defines how users interact with the database for reading, writing, and updating data. A well-designed architecture ensures **data consistency**, **performance**, and **security**.  
The main types are:

#### 1. 1-Tier Architecture
The client, server, and database are all on the same system. Suitable for personal or standalone applications.  
*Example:* Microsoft Excel.

**Advantages:**
- Simple and cost-effective
- Easy to implement

**Disadvantages:**
- Single-user limitation
- Poor security
- No centralized control

**Illustration:**  
![DBMS 1-Tier Architecture](https://media.geeksforgeeks.org/wp-content/uploads/20230509110722/DBMS-1-Tier-Architecture.webp)

#### 2. 2-Tier Architecture
A client-server model where the application (client) communicates directly with the database server.  
*Example:* Library Management System.

**Advantages:**
- Easy access and deployment
- Scalable and low cost

**Disadvantages:**
- Limited scalability with many users
- Security risks due to direct database access
- Tight coupling between client and database

**Illustration:**  
![DBMS 2-Tier Architecture](https://media.geeksforgeeks.org/wp-content/uploads/20250108093805302915/2_tier.webp)

#### 3. 3-Tier Architecture
Adds an **application server** between the client and database. The client interacts with the application server, which communicates with the database. Common in large web applications.  
*Example:* E-commerce websites.

**Advantages:**
- Enhanced scalability and security
- Better data integrity

**Disadvantages:**
- More complex and costly
- Slower response time due to extra layer

**Illustration:**  
![DBMS 3-Tier Architecture](https://media.geeksforgeeks.org/wp-content/uploads/20250108093901256398/3_tier.webp)

---

### Database Users

#### 1. Database Administrator (DBA):

**Definition:**
A DBA is the person responsible for managing and maintaining the database system.

**Main Duties:**

- Installing and configuring the DBMS.
- Creating and managing databases.
- Setting up user accounts, roles, and permissions.
- Ensuring data security, backup, and recovery.
- Monitoring database performance and fixing issues.

**Example:**
A DBA ensures that the company's MySQL or Oracle database runs smoothly and securely every day.

#### 2. Database Developer / Application Programmer:

**Definition:**
A Database Developer (or Application Programmer) is someone who designs, develops, and writes programs that interact with the database.

**Main Duties:**

- Designing database schemas (tables, relationships, keys).
- Writing SQL queries, stored procedures, and triggers.
- Developing applications or APIs that use the database.
- Ensuring the software efficiently stores and retrieves data.

**Example:**
A developer writing a web app that uses SQL queries to fetch user data from a database.

#### 3. End Users:

**Definition:**
End users are the people who use the database applications to perform their daily tasks. They don't manage or design the database — they just use it.

**Types of End Users:**

- **Casual Users:** Occasionally query the database using reports or dashboards.
- **Naive Users:** Use predefined forms or applications (like ATM users).
- **Sophisticated Users:** Use complex queries and analysis tools.
- **Standalone Users:** Maintain their own personal databases (like Excel or Access).

**Example:**
A bank customer using an ATM or a student checking their result online — both are end users interacting with a database indirectly.

---

### What is Data Independence?

**Definition:**
Data Independence means that changes made in one level of the database schema do not affect the higher levels.

It allows us to modify the database structure (like storage or tables) without changing the application programs that use the data.

In other words —

You can change how data is stored or organized without changing how users access it.

There are two types of data independence:

#### 1️⃣ Physical Data Independence

**Definition:**
The ability to change the physical (internal) storage of data without affecting the logical (conceptual) schema.

**In simple words:**
You can change how data is stored (e.g., file format, indexing, compression) without changing what data is stored.

**Example:**
If you move data from a hard disk to cloud storage or add an index for faster search, the logical view (tables, relationships) remains the same — applications still work normally.

**Goal:**
To shield the conceptual schema from changes in the internal schema.

#### 2️⃣ Logical Data Independence

**Definition:**
The ability to change the logical (conceptual) schema without affecting the external (user/view) schemas.

**In simple words:**
You can change what data is stored (like adding/removing columns or tables) without changing how users see it.

**Example:**
If you add a new column email in the Student table, users who only view name and marks don't need to change anything in their applications.

**Goal:**
To protect user views (external schema) from changes in the conceptual schema.

---

## 2. Relational Model

### What is a Relation (Table)?

**Definition:**
In a Relational Database, a Relation is simply a table that stores data in rows and columns.
Each row (tuple) represents one record, and each column (attribute) represents a property or field of that record.

**Example:**

| Student_ID | Name  | Age | Course |
|------------|-------|-----|--------|
| 101        | Arjun | 20  | B.Tech |
| 102        | Meera | 21  | BCA    |
| 103        | Ravi  | 22  | B.Sc   |

Here, the table Student is a Relation.

#### 1️⃣ Tuples (Rows):

**Definition:**
A tuple is a single row or record in a table.
It represents one instance of data in the relation.

**Example:**
(101, Arjun, 20, B.Tech) → one tuple representing one student.

#### 2️⃣ Attributes (Columns):

**Definition:**
An attribute is a column in a table that represents a specific property or field of the entity.

**Example:**
Student_ID, Name, Age, and Course are attributes of the Student table.

#### 3️⃣ Degree:

**Definition:**
The degree of a relation is the number of attributes (columns) in that table.

**Example:**
In the above Student table, there are 4 attributes, so degree = 4.

#### 4️⃣ Cardinality:

**Definition:**
The cardinality of a relation is the number of tuples (rows) in that table.

**Example:**
In the Student table, there are 3 rows, so cardinality = 3.

---

### Keys in DBMS

**Definition:**
Keys are special fields or combinations of fields used to uniquely identify records in a database table and to establish relationships between tables.

#### 1️⃣ Super Key

**Definition:**
A Super Key is any set of one or more attributes that uniquely identifies a record in a table.
It may contain extra/unnecessary attributes.

**Example:**
For a table Student(Student_ID, Name, Email):

{Student_ID}, {Email}, {Student_ID, Email} — all are Super Keys.

#### 2️⃣ Candidate Key

**Definition:**
A Candidate Key is a minimal super key, meaning it uniquely identifies a record but has no unnecessary attributes.
It is the best possible key to act as a primary key.

**Example:**
If {Student_ID} and {Email} both uniquely identify students →
Both are Candidate Keys.

#### 3️⃣ Primary Key

**Definition:**
A Primary Key is the main key chosen from the candidate keys to uniquely identify each record in a table.
It cannot contain NULL values and must be unique.

**Example:**
Student_ID can be chosen as the Primary Key.

#### 4️⃣ Alternate Key

**Definition:**
A Candidate Key that is not selected as the primary key is called an Alternate Key.

**Example:**
If Student_ID is Primary Key → then Email becomes an Alternate Key.

#### 5️⃣ Foreign Key

**Definition:**
A Foreign Key is a field in one table that refers to the Primary Key of another table.
It is used to maintain relationships between tables.

**Example:**

```
Student(Student_ID, Name)
Marks(Student_ID, Score)
```

Here, Marks.Student_ID is a Foreign Key referencing Student.Student_ID.

#### 6️⃣ Composite Key

**Definition:**
A Composite Key is a combination of two or more attributes that together uniquely identify a record.

**Example:**
In a table Enrollment(Student_ID, Course_ID, Date),
→ (Student_ID, Course_ID) together form a Composite Key.

#### 7️⃣ Surrogate Key

**Definition:**
A Surrogate Key is an artificial key (usually auto-generated) used when no natural key exists or suitable.
It has no business meaning.

**Example:**
Student_ID = 1001, 1002, 1003 (auto-generated by the system).

---

### Integrity Constraints

**Definition:**
Integrity constraints are rules that ensure the accuracy and consistency of data in a database.

#### 1️⃣ Entity Integrity

**Definition:**
Ensures that each row in a table is uniquely identified — hence the Primary Key cannot be NULL.

**Example:**
In Student table, Student_ID (Primary Key) must not be NULL.

#### 2️⃣ Referential Integrity

**Definition:**
Ensures that a Foreign Key value always refers to an existing Primary Key in another table.
It prevents orphan records.

**Example:**
If Marks.Student_ID = 105 → there must be a record with Student.Student_ID = 105.

#### 3️⃣ Domain Integrity

**Definition:**
Ensures that data values are valid and within a defined range or format for a given attribute.

**Example:**

- Age must be between 0 and 100
- Email must follow a valid email format

---

## 3. ER Model (Entity-Relationship Model)

The **ER Model** is a conceptual framework for database design.  
It visually represents entities, their attributes, and the relationships between them through **Entity-Relationship Diagrams (ERDs)**.

### Components of ER Diagram
![Components of ER Diagram](https://media.geeksforgeeks.org/wp-content/uploads/20230428090323/Introduction-to-ER-Model-1.webp)

- **Entity**: Real-world object/concept stored as data (e.g., Student, Course).
- **Attribute**: Properties describing an entity (e.g., StudentID, CourseName).
- **Relationship**: Association between entities (e.g., Student enrolls in Course).

### Why Use ER Diagrams
- Easy conversion into relational tables.
- Models real-world objects in a clear way.
- Requires no technical DBMS knowledge to understand.
- Simplifies complex systems into visual form.

### Symbols in ER Model
![Symbols used in ER Diagram](https://media.geeksforgeeks.org/wp-content/uploads/20230428115454/Introduction-to-ER-Model-2-768.webp)

- **Rectangle**: Entity
- **Ellipse**: Attribute
- **Diamond**: Relationship
- **Line**: Connects entities/attributes
- **Double Ellipse**: Multivalued attribute
- **Double Rectangle**: Weak entity

### Entities

#### What is an Entity?
- Real-world object/concept about which data is stored.
- **Entity Type**: Structure definition (e.g., Student table).
- **Entity Instance**: A single occurrence (row in table).

#### Entity Set
- Collection of all entities of a specific type.

### Types of Entities
![Strong Entity and Weak Entity](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20210219121849/12310.png)

1. **Strong Entity**
   - Has its own unique key attribute.
   - Does not depend on another entity.
   - Represented by **rectangle**.

2. **Weak Entity**
   - Cannot be uniquely identified without a related strong entity.
   - Depends on an identifying relationship with a strong entity.
   - Represented by **double rectangle**.

### Attributes
![Entity and Attributes](https://media.geeksforgeeks.org/wp-content/uploads/20250517122835356955/studn-dbms.png)

- **Key Attribute**: Uniquely identifies each entity (underlined oval).
- **Composite Attribute**: Composed of multiple sub-attributes.
- **Multivalued Attribute**: Can store multiple values for an entity (double oval).
- **Derived Attribute**: Calculated from other attributes (dashed oval).

### Degree of Relationship (Number of entity sets in relationship)
1. **Unary** – 1 entity set involved.
2. **Binary** – 2 entity sets involved.
3. **Ternary** – 3 entity sets involved.
4. **N-ary** – n entity sets involved.

### Cardinality in ER Model
Defines maximum number of relationships per entity.

#### 1. One-to-One
![One to One Cardinality](https://media.geeksforgeeks.org/wp-content/uploads/20230920133529/onetoone.jpg)  
![Set Representation of One-to-One](https://media.geeksforgeeks.org/wp-content/uploads/20220131223352/121.jpg)

- Each entity relates to only one entity in the other set.

#### 2. One-to-Many
![One to Many Cardinality](https://media.geeksforgeeks.org/wp-content/uploads/20230920133617/onetomany.jpg)  
![Set Representation of One-to-Many](https://media.geeksforgeeks.org/wp-content/uploads/20230428115353/12n.webp)

- One entity can relate to multiple entities in the other set.

#### 3. Many-to-One
![Many to One Cardinality](https://media.geeksforgeeks.org/wp-content/uploads/20230920133703/manytoone.jpg)  
![Set Representation of Many-to-One](https://media.geeksforgeeks.org/wp-content/uploads/20220131232355/m21.jpg)

- Multiple entities relate to one entity in the other set.

#### 4. Many-to-Many
![Many to Many Cardinality](https://media.geeksforgeeks.org/wp-content/uploads/20230920133746/manytomany.jpg)  
![Many-to-Many Set Representation](https://media.geeksforgeeks.org/wp-content/uploads/20220208105038/manytomantrelationship.jpg)

- Entities from both sets can have multiple relationships with each other.

---

## 4. Normalization (Data Organization)

### What is Normalization? Why is it Important in DBMS?

**Definition:**  
Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity.  
It involves splitting large tables into smaller, related tables and defining relationships between them.

**Importance of Normalization:**
- Eliminates redundant data.
- Prevents anomalies during insert, update, and delete operations.
- Improves data integrity and consistency.

### What is Denormalization? How Does it Differ from Normalization?

**Definition:**  
Denormalization is the process of combining tables to improve query performance, often at the cost of introducing redundancy.  

**Difference:**

| Aspect         | Normalization                           | Denormalization                           |
|----------------|----------------------------------------|--------------------------------------------|
| Goal           | Minimize redundancy, improve integrity | Improve performance for read-heavy tasks  |
| Data Redundancy| Reduced                                | Increased                                 |
| Use Case       | Transactional systems                  | Analytical / reporting systems            |

---

### Types of Normal Forms

#### 1. First Normal Form (1NF) – Eliminating Duplicate Records
- Columns contain **atomic values**.
- No repeating groups or arrays.
- Each row is unique.

**Example Violation:**  
A single cell storing multiple phone numbers → split into separate rows.

#### 2. Second Normal Form (2NF) – Eliminating Partial Dependency
- Must be in **1NF**.
- No partial dependency (non-key attributes depend on **entire** primary key).
- In 2NF, every non-prime attribute must be fully functionally dependent on the whole of every candidate key — it must not depend on just a part of any composite candidate key.

**Example Violation:**  
For `(StudentID, CourseID)` as key, `StudentName` depends only on `StudentID` → move `StudentName` to separate table.

#### 3. Third Normal Form (3NF) – Eliminating Transitive Dependency
A relation is in **3NF** if:

1. It is already in **2NF**.
2. **No transitive dependency** exists — i.e., a **non-prime attribute** must **not** depend on another **non-prime attribute**.
3. **Equivalently:** For every functional dependency `X → Y` in the table, at least one of these must be true:
   - **X** is a **superkey** (meaning it can uniquely identify a row), **or**
   - **Y** is a **prime attribute** (part of some candidate key).

**Example Violation:**  
If `Instructor` depends on `CourseID`, which depends on `StudentID` → move `Instructor` to table linked by `CourseID`.

#### 4. Boyce–Codd Normal Form (BCNF) – Strongest 3NF
- Must be in **3NF**.
- For every dependency `X → Y`, **X must be a superkey**.

**Example Violation:**  
If `(StudentID, CourseID) → Instructor` but neither `StudentID` nor `CourseID` is a superkey → decompose the table.

![BCNF](https://media.geeksforgeeks.org/wp-content/uploads/20250108151038174913/bcnf.webp)

#### 5. Fourth Normal Form (4NF) – Removing Multi-Valued Dependencies
- Must be in **BCNF**.
- No multi-valued dependencies.

**Example Violation:**  
If `(StudentID, Language, Hobby)` exists with independent languages & hobbies → split into separate `Language` and `Hobby` tables.

#### 6. Fifth Normal Form (5NF) – Eliminating Join Dependency
- Must be in **4NF**.
- All join dependencies removed without losing information.

### Advantages of Normalization
1. Reduces redundancy.
2. Improves consistency.
3. Simplifies design.
4. Improves query performance.
5. Easier maintenance.
6. Facilitates scalability.
7. Better data modeling.
8. Prevents update anomalies.
9. Improves security & integrity.
10. Optimizes storage usage.

### Challenges of Over-Normalization
- Complex queries with many joins.
- Possible performance overhead in large systems.

**When to Use:**
- **Normalization:** Transaction-heavy systems (e.g., banking).
- **Denormalization:** Read-heavy systems (e.g., data warehousing).

### Normal Forms Summary Table

| Normal Form | Rule / Condition | Purpose |
|-------------|------------------|---------|
| **1NF (First Normal Form)** | No repeating groups or arrays; each cell contains atomic (indivisible) values. | Remove duplicate columns and ensure atomicity. |
| **2NF (Second Normal Form)** | Must be in 1NF **and** all non-key attributes must be fully dependent on the primary key (no partial dependency). | Remove partial dependency in composite keys. |
| **3NF (Third Normal Form)** | Must be in 2NF **and** no transitive dependency (non-key attributes should not depend on other non-key attributes). | Remove transitive dependencies. |
| **BCNF (Boyce-Codd Normal Form)** | Must be in 3NF **and** every determinant must be a candidate key. | Handle anomalies not covered by 3NF. |
| **4NF (Fourth Normal Form)** | Must be in BCNF **and** no multi-valued dependencies. | Eliminate multi-valued dependency issues. |
| **5NF (Fifth Normal Form)** | Must be in 4NF **and** no join dependency (table should not be decomposable without loss of data). | Ensure lossless decomposition. |

---

### Normal Forms Examples with Conflicts & Resolutions

#### **1NF (First Normal Form)**
**Rule:**  
- Only **atomic values** (no repeating groups or multi-valued attributes)  
- No composite attributes  
- No duplicate rows  

**Conflicting Table (Not in 1NF):**
| StudentID | Name     | Phone Numbers         |
|-----------|----------|-----------------------|
| 1         | Alice    | 12345, 67890           |
| 2         | Bob      | 55555                  |

**Issue:**  
`Phone Numbers` column contains multiple values (multi-valued attribute).

**Resolved Table (1NF):**
| StudentID | Name     | Phone Number |
|-----------|----------|--------------|
| 1         | Alice    | 12345        |
| 1         | Alice    | 67890        |
| 2         | Bob      | 55555        |

---

#### **2NF (Second Normal Form)**
**Rule:**  
- Must be in **1NF**  
- **No partial dependency** (No non-prime attribute should depend on part of a composite key)

**Conflicting Table (1NF but not 2NF):**
| StudentID | CourseID | StudentName | CourseName |
|-----------|----------|-------------|------------|
| 1         | C1       | Alice       | DBMS       |
| 1         | C2       | Alice       | OS         |

**Issue:**  
- Candidate key = `(StudentID, CourseID)`  
- `StudentName` depends **only** on `StudentID`  
- `CourseName` depends **only** on `CourseID` → **Partial dependency**

**Resolved Tables (2NF):**

**Student Table:**
| StudentID | StudentName |
|-----------|-------------|
| 1         | Alice       |

**Course Table:**
| CourseID  | CourseName  |
|-----------|-------------|
| C1        | DBMS        |
| C2        | OS          |

**Enrollment Table:**
| StudentID | CourseID |
|-----------|----------|
| 1         | C1       |
| 1         | C2       |

---

#### **3NF (Third Normal Form)**
**Rule:**  
- Must be in **2NF**  
- No **transitive dependency** (No non-prime attribute depends on another non-prime attribute)

**Conflicting Table (2NF but not 3NF):**
| StudentID | StudentName | DeptID | DeptName  |
|-----------|-------------|--------|-----------|
| 1         | Alice       | D1     | Computer  |
| 2         | Bob         | D2     | Physics   |

**Issue:**  
- Candidate key = `StudentID`  
- `DeptName` depends on `DeptID` (which is a non-prime attribute) → **Transitive dependency**

**Resolved Tables (3NF):**

**Student Table:**
| StudentID | StudentName | DeptID |
|-----------|-------------|--------|
| 1         | Alice       | D1     |
| 2         | Bob         | D2     |

**Department Table:**
| DeptID | DeptName  |
|--------|-----------|
| D1     | Computer  |
| D2     | Physics   |

---

#### **4NF (Fourth Normal Form)**
**Rule:**  
- Must be in **Boyce–Codd Normal Form (BCNF)**  
- No **multi-valued dependencies** (MVDs) unless trivial  

**Conflicting Table (3NF/BCNF but not 4NF):**
| StudentID | Hobby       | Language |
|-----------|-------------|----------|
| 1         | Chess       | English  |
| 1         | Chess       | French   |
| 1         | Painting    | English  |
| 1         | Painting    | French   |

**Issue:**  
- `Hobby` and `Language` are **independent multi-valued facts** about `StudentID`  
- This leads to redundant combinations

**Resolved Tables (4NF):**

**StudentHobby Table:**
| StudentID | Hobby     |
|-----------|-----------|
| 1         | Chess     |
| 1         | Painting  |

**StudentLanguage Table:**
| StudentID | Language  |
|-----------|-----------|
| 1         | English   |
| 1         | French    |

---

### Anomalies (Insertion, Deletion, Update)

**Definition:**

Anomalies are problems or inconsistencies that occur in a database due to improper table design — typically when data is stored in a single large unnormalized table instead of being divided into smaller related tables.

These anomalies lead to data redundancy, inconsistency, and integrity issues.

There are three main types of anomalies:

#### 1️⃣ Insertion Anomaly

**Definition:**
Occurs when you cannot insert data into a table because some other data is missing.

**Example:**
Consider a table combining Student and Course details:

| Student_ID | Student_Name | Course_ID | Course_Name |
|------------|--------------|-----------|-------------|
| 101        | Arjun        | C1        | DBMS        |
| 102        | Meera        | C2        | SQL         |

Now, suppose a new course "Python" is introduced, but no student has enrolled yet.
➡️ You cannot insert this course record because the table requires a Student_ID and Student_Name.

**Problem:**
We can't add a new course without a student.

**✅ Solution:**
Split into two tables — Student and Course, linked by Enrollment.

#### 2️⃣ Deletion Anomaly

**Definition:**
Occurs when deleting one piece of data unintentionally removes other important data.

**Example:**
Using the same table, if student Arjun (101) drops the DBMS course and his record is deleted:
➡️ The course DBMS information is also lost, even though the course still exists.

**Problem:**
Deleting a student record causes loss of course data.

**✅ Solution:**
Separate the course information into its own table.

#### 3️⃣ Update Anomaly

**Definition:**
Occurs when the same data is stored multiple times, and an update in one place requires manual updates everywhere — otherwise, inconsistencies occur.

**Example:**
If the course name "DBMS" changes to "Database Systems",
➡️ You must update it in every row where that course appears.
If you miss one, data becomes inconsistent.

**Problem:**
Data redundancy causes inconsistency on updates.

**✅ Solution:**
Store course details in a separate table and reference it by ID.

---

## 5. SQL Basics (Foundation)

### What is SQL?
SQL (Structured Query Language) is a standard language used to interact with relational databases.  
It allows you to **create**, **read**, **update**, and **delete** data (CRUD operations) and manage database structures.

---

### SQL vs MySQL vs PostgreSQL vs Oracle

#### **1. SQL**
- A *language*, not a database.
- Used to write queries like `SELECT`, `INSERT`, `UPDATE`.

#### **2. MySQL**
- An open-source **RDBMS**.
- Fast, widely used for web applications.
- Follows SQL but has its own extensions.
- Great for read-heavy workloads.

#### **3. PostgreSQL**
- Advanced, open-source **object-relational** database.
- Supports JSON, indexing techniques, triggers, stored procedures.
- Strong ACID compliance, best for complex queries.

#### **4. Oracle Database**
- Enterprise-grade commercial database.
- Highly scalable, secure, supports huge transactions.
- Used by large companies (finance, telecom, enterprise systems).

---

### SQL Categories

#### **1. DDL – Data Definition Language**
Used to define or modify database structure.

- `CREATE` – Create tables/databases  
- `ALTER` – Modify table structure  
- `DROP` – Delete table/database  
- `TRUNCATE` – Delete all rows (faster than DELETE)

**Example:**
```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);
```

---

#### **2. DML – Data Manipulation Language**
Used to manipulate data inside tables.

- `INSERT` – Add new rows  
- `UPDATE` – Modify existing rows  
- `DELETE` – Remove rows  
- `SELECT` – Read data

**Example:**
```sql
INSERT INTO users VALUES (1, 'Purvesh');
```

---

#### **3. DCL – Data Control Language**
Used to control access/permissions.

- `GRANT` – Give access  
- `REVOKE` – Remove access

**Example:**
```sql
GRANT SELECT ON users TO 'student';
```

---

#### **4. TCL – Transaction Control Language**
Used to manage transactions.

- `COMMIT` – Save changes  
- `ROLLBACK` – Undo changes  
- `SAVEPOINT` – Mark a spot to rollback to

**Example:**
```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 500 WHERE id = 1;
SAVEPOINT s1;
UPDATE accounts SET balance = balance + 500 WHERE id = 2;
ROLLBACK TO s1;
COMMIT;
```

---

### SQL Data Types (Most Common)

- **INT** – Whole numbers  
- **FLOAT / DOUBLE** – Decimal numbers  
- **VARCHAR(n)** – Variable-length string  
- **CHAR(n)** – Fixed length string  
- **DATE** – YYYY-MM-DD  
- **DATETIME / TIMESTAMP** – Date + time  
- **BOOLEAN** – True/False  
- **TEXT** – Long text

---

### SQL Constraints

#### **PRIMARY KEY**
- Uniquely identifies each row (no duplicates, no NULL).

#### **FOREIGN KEY**
- Creates relationship between tables; references another table's primary key.

#### **UNIQUE**
- No duplicate values allowed.

#### **CHECK**
- Enforces a condition on a column.

#### **DEFAULT**
- Sets default value if no value provided.

#### **NOT NULL**
- Column cannot store NULL values.

**Example:**
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE NOT NULL,
    salary INT CHECK (salary > 0),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(id)
);
```

---

## 6. Querying Data

### SELECT Statement
Used to retrieve data from a table.

**Syntax:**
```sql
SELECT column1, column2 FROM table_name;
```

**Example:**
```sql
SELECT name, age FROM students;
```

---

### DISTINCT
Removes duplicate values from the result.

**Example:**
```sql
SELECT DISTINCT city FROM customers;
```

---

### Filtering Data – WHERE Clause
Used to filter rows based on a condition.

**Example:**
```sql
SELECT * FROM employees WHERE salary > 50000;
```

---

### BETWEEN (Range Filter)
Filters values within a range (inclusive).

**Example:**
```sql
SELECT * FROM orders 
WHERE order_date BETWEEN '2024-01-01' AND '2024-12-31';
```

---

### IN (Match any of given values)
Useful when matching multiple possible values.

**Example:**
```sql
SELECT * FROM students 
WHERE department IN ('IT', 'CSE', 'ECE');
```

---

### LIKE (Pattern Matching)
Used for searching text with patterns.

**Wildcards:**
- `%` → multiple characters  
- `_` → single character

**Examples:**
```sql
SELECT * FROM users WHERE name LIKE 'P%';   -- starts with P
SELECT * FROM users WHERE name LIKE '%sh';  -- ends with sh
SELECT * FROM users WHERE name LIKE '_a%';  -- second letter is 'a'
```

---

### IS NULL / IS NOT NULL
Checks for NULL values.

**Example:**
```sql
SELECT * FROM employees WHERE manager_id IS NULL;
```

---

### ORDER BY – Sorting Data
Sort results in **ascending (ASC)** or **descending (DESC)** order.

**Examples:**
```sql
SELECT * FROM products ORDER BY price ASC;
SELECT * FROM products ORDER BY rating DESC;
```

---

### LIMIT / TOP – Limiting Results
Different databases use different keywords:

**MySQL / PostgreSQL:**
```sql
SELECT * FROM students LIMIT 5;
```

**SQL Server:**
```sql
SELECT TOP 5 * FROM students;
```

---

### Aliases (AS)
Used to give temporary names to columns or tables.

**Column Alias:**
```sql
SELECT name AS student_name FROM students;
```

**Table Alias:**
```sql
SELECT s.name, d.dept_name
FROM students AS s
JOIN departments AS d ON s.dept_id = d.id;
```

---

## 7. Aggregate Functions

### 1. Aggregate Functions
Aggregate functions perform calculations on a group of values and return a single result.

#### **COUNT()**
Returns number of rows.

```sql
SELECT COUNT(*) FROM employees;
```

#### **SUM()**
Adds all numeric values.

```sql
SELECT SUM(salary) FROM employees;
```

#### **AVG()**
Returns the average value.

```sql
SELECT AVG(salary) FROM employees;
```

#### **MIN()**
Returns the smallest value.

```sql
SELECT MIN(age) FROM students;
```

#### **MAX()**
Returns the largest value.

```sql
SELECT MAX(price) FROM products;
```

---

### 2. GROUP BY
Used to group rows that have the same values in one or more columns.
Often used with aggregate functions.

**Example:**
```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```
→ Returns average salary of each department.

---

### 3. HAVING Clause
Used to filter groups **after** applying aggregation.

**Example:**
```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```
→ Shows only departments where average salary is above 50k.

---

### 4. WHERE vs HAVING – Key Difference

| Feature | WHERE | HAVING |
|--------|--------|--------|
| **Purpose** | Filters rows before grouping | Filters groups after grouping |
| **Used With** | Tables and rows | GROUP BY + aggregates |
| **Can use aggregates?** | ❌ No | ✅ Yes |
| **Order of execution** | First | After GROUP BY |

**Example Showing Difference:**

```sql
-- Filter rows using WHERE
SELECT department, COUNT(*)
FROM employees
WHERE salary > 30000
GROUP BY department;

-- Filter groups using HAVING
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 10;
```

---

## 8. Joins

### Joins in SQL

**Definition:**  
A **JOIN** in SQL is an operation that combines columns from two or more tables based on a **related column** between them.  
It is used to query and retrieve data from multiple tables in a relational database.

---

### Types of Joins

#### 1. **INNER JOIN**  
Returns only the rows where there is a match in both tables.  

**Example:**
```sql
SELECT * 
FROM Student
INNER JOIN Course 
    ON Student.ID = Course.StudentID;
```

#### 2. **LEFT JOIN (LEFT OUTER JOIN)**  
Returns all rows from the **left** table and matching rows from the right table.  
If no match exists, NULL values are returned for columns from the right table.

**Example:**
```sql
SELECT * 
FROM Student
LEFT JOIN Course 
    ON Student.ID = Course.StudentID;
```

#### 3. **RIGHT JOIN (RIGHT OUTER JOIN)**  
Returns all rows from the **right** table and matching rows from the left table.  
If no match exists, NULL values are returned for columns from the left table.

**Example:**
```sql
SELECT * 
FROM Student
RIGHT JOIN Course 
    ON Student.ID = Course.StudentID;
```

#### 4. **FULL JOIN (FULL OUTER JOIN)**  
Returns all rows when there is a match in **either** left or right table.  
If no match exists, NULL values are returned for columns of the table without a match.

**Example:**
```sql
SELECT * 
FROM Student
FULL JOIN Course 
    ON Student.ID = Course.StudentID;
```

#### 5. **CROSS JOIN**  
Returns the **Cartesian product** of two tables — every combination of rows from both tables.

**Example:**
```sql
SELECT * 
FROM Student
CROSS JOIN Course;
```

#### 6. **SELF JOIN**  
Joins a table with itself, useful for comparing rows in the same table.  
Uses table aliases to differentiate instances.

**Example:**
```sql
SELECT E1.Employee_ID, E1.Employee_Name, E2.Employee_Name AS Manager_Name
FROM Employee E1
LEFT JOIN Employee E2 
    ON E1.Manager_ID = E2.Employee_ID;
```

---

## 9. Subqueries

### What is a Subquery?
A **subquery** (or inner query) is a query inside another query.  
It is used to fetch data needed by the outer query.

Subqueries can be used in:
- `SELECT`
- `FROM`
- `WHERE`
- `HAVING`
- `INSERT`, `UPDATE`, `DELETE` (sometimes)

---

### 1. Single-Row Subquery
A subquery that returns **exactly one row**.

Used with: `=`, `<`, `>`, `<=`, `>=`

**Example:**
```sql
SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary) FROM employees
);
```
→ Compares salary with a single value (average salary).

---

### 2. Multi-Row Subquery
Returns **multiple rows**.

Used with operators like:
- `IN`
- `ANY`
- `ALL`

---

#### (a) IN (Match any value)
```sql
SELECT name
FROM students
WHERE dept_id IN (
    SELECT id
    FROM departments
    WHERE location = 'Pune'
);
```

---

#### (b) ANY (True if ANY one value matches condition)
```sql
SELECT name
FROM employees
WHERE salary > ANY (
    SELECT salary FROM interns
);
```
→ Salary greater than **at least one** intern's salary.

---

#### (c) ALL (True if condition matches ALL values)
```sql
SELECT name
FROM employees
WHERE salary > ALL (
    SELECT salary FROM interns
);
```
→ Salary greater than **every** intern's salary.

---

### 3. Correlated Subquery
A subquery that **depends on the outer query** for each row.

Runs once per outer-row → slower but powerful.

**Example:**
```sql
SELECT e1.name
FROM employees e1
WHERE e1.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department = e1.department
);
```
→ For each employee, calculate department-wise average.

---

### 4. Subqueries in Different Clauses

#### (a) Subquery in SELECT
Used to compute extra values.

```sql
SELECT name,
       (SELECT COUNT(*) FROM orders WHERE orders.emp_id = employees.id) AS order_count
FROM employees;
```

---

#### (b) Subquery in FROM (Inline View/Table Subquery)
Acts like a temporary table.

```sql
SELECT dept, avg_sal
FROM (
    SELECT department AS dept, AVG(salary) AS avg_sal
    FROM employees
    GROUP BY department
) AS dept_avg;
```

---

#### (c) Subquery in WHERE (Most common)
Used for filtering.

```sql
SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary) FROM employees
);
```

---

## 10. Set Operations

### What Are Set Operations?
Set operations combine the results of two SELECT queries.  
Both queries **must have the same number of columns** and matching data types.

---

### 1. UNION vs UNION ALL

#### UNION
- Combines results of two SELECT queries.
- **Removes duplicates**.
- Performs a **sorting** step → slightly slower.

**Example:**
```sql
SELECT name FROM table1
UNION
SELECT name FROM table2;
```

---

#### UNION ALL
- Combines results of two SELECT queries.
- **Keeps duplicates**.
- Faster than UNION (no sorting).

**Example:**
```sql
SELECT name FROM table1
UNION ALL
SELECT name FROM table2;
```

---

### 2. INTERSECT
Returns **common rows** between two result sets (like set intersection).

Supported in:
- PostgreSQL
- Oracle
- SQL Server  
(Not directly in MySQL — needs workaround using INNER JOIN.)

**Example:**
```sql
SELECT email FROM customers_2024
INTERSECT
SELECT email FROM customers_2025;
```
→ Returns emails present in both tables.

---

### 3. EXCEPT / MINUS
Removes rows from the first query that appear in the second query.

- **EXCEPT** → Used in PostgreSQL, SQL Server  
- **MINUS** → Used in Oracle  
- MySQL: Use LEFT JOIN trick to simulate.

**Example (EXCEPT):**
```sql
SELECT id FROM tableA
EXCEPT
SELECT id FROM tableB;
```
→ Shows ids present in A but not in B.

**Example (Oracle MINUS):**
```sql
SELECT id FROM tableA
MINUS
SELECT id FROM tableB;
```

---

## 11. Functions in SQL

SQL provides built-in functions for string manipulation, dates, and numeric calculations.

---

### 1. String Functions

#### **LENGTH()**
Returns the number of characters in a string.
```sql
SELECT LENGTH('Purvesh');
```

#### **CONCAT()**
Combines multiple strings.
```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM employees;
```

#### **SUBSTRING()** (or SUBSTR)
Extracts part of a string.
```sql
SELECT SUBSTRING('LearnPlay', 1, 5);   -- Learn
```

#### **UPPER() / LOWER()**
Converts text to uppercase or lowercase.
```sql
SELECT UPPER(name), LOWER(name) FROM students;
```

#### **TRIM()**
Removes leading and trailing spaces.
```sql
SELECT TRIM('   Hello   ');
```

#### **REPLACE()**
Replaces part of a string with another value.
```sql
SELECT REPLACE('JavaScript', 'Java', 'Type'); -- TypeScript
```

---

### 2. Date Functions

#### **NOW()**
Returns current date + time.
```sql
SELECT NOW();
```

#### **CURDATE()**
Returns the current date.
```sql
SELECT CURDATE();
```

#### **DATEDIFF()**
Returns days between two dates.
```sql
SELECT DATEDIFF('2025-12-31', '2025-01-01');
```

#### **YEAR(), MONTH(), DAY()**
Extracts year, month, day from a date.
```sql
SELECT YEAR(order_date), MONTH(order_date), DAY(order_date)
FROM orders;
```

---

### 3. Numeric Functions

#### **ROUND()**
Rounds a number to a specified decimal.
```sql
SELECT ROUND(12.5678, 2);  -- 12.57
```

#### **CEIL()**
Rounds number **up** to nearest integer.
```sql
SELECT CEIL(10.2);  -- 11
```

#### **FLOOR()**
Rounds number **down**.
```sql
SELECT FLOOR(10.9);  -- 10
```

#### **ABS()**
Returns absolute value.
```sql
SELECT ABS(-50);  -- 50
```

#### **MOD()**
Returns remainder of division (x % y).
```sql
SELECT MOD(17, 5);  -- 2
```

---

**End of Document**
