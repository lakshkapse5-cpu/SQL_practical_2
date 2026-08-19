# Student Course Management Database

## 📌 Overview

This project is a **Student Course Management Database** created using SQL. It demonstrates how to create and connect multiple tables using **Primary Keys, Foreign Keys, UNIQUE constraints, NOT NULL constraints, and CHECK constraints**.

The database stores information about:

* 🏢 Departments
* 👨‍🎓 Students
* 📚 Courses
* 📝 Student Enrollments and Grades

---

## 🗂️ Database Structure

The database consists of four tables:

### 1. `department`

Stores information about academic departments.

| Column      | Data Type   | Description          |
| ----------- | ----------- | -------------------- |
| `dept_id`   | INT         | Unique department ID |
| `dept_name` | VARCHAR(50) | Department name      |

**Constraints:**

* `dept_id` → Primary Key
* `dept_name` → UNIQUE and NOT NULL

---

### 2. `s` — Students

Stores student information.

| Column      | Data Type   | Description                |
| ----------- | ----------- | -------------------------- |
| `roll_no`   | INT         | Unique student roll number |
| `name`      | VARCHAR(50) | Student name               |
| `email`     | VARCHAR(50) | Student email              |
| `aadhar_no` | VARCHAR(12) | Student Aadhaar number     |
| `dept_id`   | INT         | Student's department       |

**Constraints:**

* `roll_no` → Primary Key
* `name` → NOT NULL
* `email` → UNIQUE
* `aadhar_no` → UNIQUE
* `dept_id` → Foreign Key referencing `department(dept_id)`

---

### 3. `c` — Courses

Stores information about courses offered by departments.

| Column        | Data Type   | Description                    |
| ------------- | ----------- | ------------------------------ |
| `course_id`   | INT         | Unique course ID               |
| `course_name` | VARCHAR(50) | Name of the course             |
| `dept_id`     | INT         | Department offering the course |

**Constraints:**

* `course_id` → Primary Key
* `course_name` → NOT NULL
* `dept_id` → Foreign Key referencing `department(dept_id)`

---

### 4. `e` — Enrollment

Stores student enrollment information and grades.

| Column      | Data Type | Description         |
| ----------- | --------- | ------------------- |
| `roll_no`   | INT       | Student roll number |
| `course_id` | INT       | Course ID           |
| `semester`  | INT       | Semester number     |
| `grade`     | CHAR(2)   | Student's grade     |

**Constraints:**

* Composite Primary Key: `roll_no`, `course_id`, `semester`
* `roll_no` → Foreign Key referencing `s(roll_no)`
* `course_id` → Foreign Key referencing `c(course_id)`
* `semester` → CHECK constraint between 1 and 8

---

## 🔗 Relationships

The tables are connected as follows:

```text
             ┌─────────────────┐
             │   department    │
             │─────────────────│
             │ dept_id (PK)    │
             │ dept_name       │
             └────────┬────────┘
                      │
              ┌───────┴───────┐
              │               │
              ▼               ▼
       ┌─────────────┐  ┌─────────────┐
       │      s      │  │      c      │
       │  Students   │  │   Courses   │
       │─────────────│  │─────────────│
       │ roll_no PK  │  │ course_id PK│
       │ name        │  │ course_name │
       │ dept_id FK  │  │ dept_id FK  │
       └──────┬──────┘  └──────┬──────┘
              │                 │
              └────────┬────────┘
                       ▼
                ┌─────────────┐
                │      e      │
                │ Enrollment  │
                │─────────────│
                │ roll_no FK  │
                │ course_id FK│
                │ semester    │
                │ grade       │
                └─────────────┘
```

---

## 🔑 SQL Concepts Used

This project demonstrates several important SQL concepts:

* **PRIMARY KEY** — uniquely identifies each record.
* **FOREIGN KEY** — establishes relationships between tables.
* **UNIQUE** — prevents duplicate values.
* **NOT NULL** — ensures a value must be provided.
* **CHECK** — restricts values according to a condition.
* **Composite Primary Key** — uses multiple columns together as a unique identifier.
* **VARCHAR** — stores variable-length text.
* **INT** — stores integer values.
* **CHAR** — stores fixed-length text.

---

## 🚀 How to Run

1. Open a SQL environment such as **MySQL Workbench**, **phpMyAdmin**, or another compatible SQL database system.
2. Create or select your database.
3. Run the SQL script.
4. The tables will be created in the following order:

```text
department
    ↓
s
    ↓
e

department
    ↓
c
    ↓
e
```

The order is important because the foreign keys depend on tables that must already exist.

---

## 📄 SQL Script

```sql
CREATE TABLE department (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50) UNIQUE NOT NULL
);

CREATE TABLE s (
    roll_no INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(50) UNIQUE,
    aadhar_no VARCHAR(12) UNIQUE,
    dept_id INT,
    FOREIGN KEY (dept_id)
        REFERENCES department (dept_id)
);

CREATE TABLE c (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50) NOT NULL,
    dept_id INT,
    FOREIGN KEY (dept_id)
        REFERENCES department (dept_id)
);

CREATE TABLE e (
    roll_no INT,
    course_id INT,
    semester INT CHECK (semester BETWEEN 1 AND 8),
    grade CHAR(2),
    PRIMARY KEY (roll_no, course_id, semester),
    FOREIGN KEY (roll_no)
        REFERENCES s (roll_no),
    FOREIGN KEY (course_id)
        REFERENCES c (course_id)
);
```

---

## 🎯 Purpose of the Project

The purpose of this project is to understand how relational databases work and how multiple tables can be connected using keys and constraints.

It can be used as a basic foundation for a **Student Management System** or **College Course Management System**.

---

## 👨‍💻 Author

**Laksh Kapse**

---

## ⭐ Future Improvements

The project can be extended by adding:

* Student attendance
* Faculty information
* Course credits
* Marks and examination results
* Semester-wise GPA/CGPA
* Student phone numbers
* Department faculty
* Course prerequisites
* SQL queries for reports and statistics

---

## 📜 License

This project is created for **educational and learning purposes**.
