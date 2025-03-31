## init
```sql

-- CREATE USER
CREATE USER intro_user IDENTIFIED BY mypassword
DEFAULT TABLESPACE SYSTEM 
TEMPORARY TABLESPACE temp
QUOTA UNLIMITED ON SYSTEM;

-- CONNECT
GRANT CONNECT TO intro_user;

-- CREATE PRIVILEGES
GRANT CREATE SESSION, GRANT ANY PRIVILEGE TO intro_user;
GRANT CREATE TABLE TO TEST;
GRANT CREATE VIEW TO TEST;
GRANT CREATE PROCEDURE TO TEST;
GRANT CREATE FUNCTION TO TEST;
GRANT CREATE TRIGGER TO TEST;
GRANT CREATE SEQUENCE TO TEST;

-- ADMIN TABLES
GRANT ALL ON table_name to TEST;

```
### Example
#### Scenario:

- Employees get a 5% bonus if their salary is < 5000, else 3%.

- Store the bonus in a variable and display it.

```SQL

DECLARE
    v_salary NUMBER := 4600;
    v_bonus NUMBER;

BEGIN

    IF v_salary < 5000 THEN
        v_bonus = v_salary * 0.05;
    ELSE
        v_bonus = v_salary * 0.03;
    END IF;

    DBMS_OUTPUT.PUT_LINE('Bonus: ' || v_bonus);
END

DECLARE
    -- v_salary NUMBER := 4600;
    v_salary NUMBER := &input_salary;
    v_bonus NUMBER;

BEGIN

    IF v_salary < 5000 THEN
        v_bonus := v_salary * 0.05;
    ELSE
        v_bonus := v_salary * 0.03;
    END IF;

    DBMS_OUTPUT.PUT_LINE('Bonus: ' || v_bonus);
END;
```

### CREATING TABLE
```SQL

CREATE TABLE EMPLOYEES (
    EMP_ID NUMBER PRIMARY KEY,
    EMP_NAME VARCHAR2(127) NOT NULL,
    SALARY NUMBER(10,2),
    HIRE_DATE DATE DEFAULT SYSDATE,
    DEPT_ID NUMBER

    -- CONSTRAINT fk_dept FOREIGN KEY (DEPT_ID) REFERENCES DEPARTMENTS(DEPT_ID)
);
```

### INSERT INFO
```SQL
INSERT INTO EMPLOYEES 
VALUES -- (1,'NAME1', 100.3,TO_DATE('2025-03-30','YYYY-MM-DD'),1);
-- (2,'NAME2', 300.3,TO_DATE('2025-03-30','YYYY-MM-DD'),1);
(3,'NAME3', 300.3,TO_DATE('2025-03-30','YYYY-MM-DD'),2);
```

### STORED PROCEDURES
```SQL
-- SYNTAX
CREATE [OR REPLACE] PROCEDURE procedure_name
    (param1 [IN|OUT|IN OUT] datatype, ...)
IS
    -- Local variable declarations
BEGIN
    -- Procedure logic
    [EXCEPTION]
        -- Error handling
END procedure_name;

-- EXAMPLE
CREATE OR REPLACE PROCEDURE UPDATE_SALARY(p_emp_id IN NUMBER, p_percent IN NUMBER)
IS
  -- Local variable declarations
BEGIN
    UPDATE EMPLOYEES
    SET SALARY = SALARY * (1 + p_percent/100)
    WHERE EMP_ID = p_emp_id;

    COMMIT;

END UPDATE_SALARY;

CALL UPDATE_SALARY(3,15);
```

### FUNCTIONS
```SQL
-- SYNTAX
CREATE [OR REPLACE] FUNCTION function_name
    (param1 [IN] datatype, ...)
    RETURN return_datatype
IS
    -- Local variable declarations
BEGIN
    -- Function logic
    RETURN value;
    
    [EXCEPTION]
        -- Error handling
END function_name;

-- EXAMPLE
CREATE OR REPLACE FUNCTION get_salary(p_emp_id IN NUMBER)
RETURN NUMBER
IS
    v_salary NUMBER;
BEGIN

    SELECT SALARY
    INTO v_salary
    FROM EMPLOYEES
    WHERE EMP_ID = p_emp_id;

    RETURN v_salary;

END get_salary;

-- CALLING
SELECT GET_SALARY(3) FROM DUAL;

DECLARE
    v_salary NUMBER;
BEGIN
    v_salary := get_employee_salary(101);
    DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary);
END;

```




