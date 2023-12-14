# README: MySQL Database Management

This README file provides detailed instructions on how to perform the following tasks in MySQL:

1. **Creating Tables with Constraints:**

   To create tables with constraints in MySQL, follow these steps:

   - **Define Table Structure:**
     Start by defining the structure of your table using the `CREATE TABLE` statement. For example:
     ```sql
     CREATE TABLE employees (
         employee_id INT PRIMARY KEY,
         first_name VARCHAR(50),
         last_name VARCHAR(50),
         department_id INT,
         CONSTRAINT fk_department FOREIGN KEY (department_id) REFERENCES departments(department_id)
     );
     ```
   - In this example, the `employees` table has a primary key (`employee_id`) and a foreign key (`department_id`) referencing the `departments` table.

   - **Adding Constraints:**
     You can add constraints like PRIMARY KEY, FOREIGN KEY, UNIQUE, CHECK, etc., during table creation or alter an existing table using the `ALTER TABLE` statement.

     Example of adding a UNIQUE constraint:
     ```sql
     ALTER TABLE employees
     ADD CONSTRAINT uc_employee_email UNIQUE (email);
     ```
     This ensures that the `email` column values are unique in the `employees` table.

2. **Optimizing Queries by Adding Indexes:**

   Indexes can significantly improve query performance. To add indexes:

   - **Single Column Index:**
     ```sql
     CREATE INDEX index_name ON table_name (column_name);
     ```
     For example:
     ```sql
     CREATE INDEX idx_employee_id ON employees (employee_id);
     ```
   - **Composite Index (Multiple Columns):**
     ```sql
     CREATE INDEX index_name ON table_name (column1, column2);
     ```
     Example:
     ```sql
     CREATE INDEX idx_employee_name ON employees (first_name, last_name);
     ```

3. **Implementing Stored Procedures and Functions:**

   - **Stored Procedures:**
     ```sql
     DELIMITER //

     CREATE PROCEDURE sp_get_employee_details (IN emp_id INT)
     BEGIN
         SELECT * FROM employees WHERE employee_id = emp_id;
     END //

     DELIMITER ;
     ```
   - **Functions:**
     ```sql
     DELIMITER //

     CREATE FUNCTION fn_calculate_bonus (salary INT) RETURNS INT
     BEGIN
         DECLARE bonus INT;
         SET bonus = salary * 0.1;
         RETURN bonus;
     END //

     DELIMITER ;
     ```

4. **Implementing Views:**

   - **Creating a View:**
     ```sql
     CREATE VIEW view_employee_details AS
     SELECT employee_id, first_name, last_name, department_name
     FROM employees
     JOIN departments ON employees.department_id = departments.department_id;
     ```

   - **Using the View:**
     ```sql
     SELECT * FROM view_employee_details WHERE department_name = 'IT';
     ```

5. **Implementing Triggers:**

   - **Creating a Trigger:**
     ```sql
     CREATE TRIGGER before_employee_insert
     BEFORE INSERT ON employees
     FOR EACH ROW
     SET NEW.creation_date = NOW();
     ```
     This trigger sets the `creation_date` column to the current timestamp before inserting a new record into the `employees` table.

   - **Example of Trigger on Update:**
     ```sql
     CREATE TRIGGER before_employee_update
     BEFORE UPDATE ON employees
     FOR EACH ROW
     SET NEW.last_updated = NOW();
     ```
     This trigger updates the `last_updated` column with the current timestamp before updating a record in the `employees` table.

Feel free to customize the provided examples according to your specific database schema and requirements.
