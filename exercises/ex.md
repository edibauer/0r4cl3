## init
### Exercise 1: Basic Salary Calculator
Objective: Create a PL/SQL block that calculates an employee's annual salary (monthly salary × 12) and displays it.

```sql
DECLARE
    v_salary NUMBER := 3000;
    v_res NUMBER;
BEGIN

    v_res := v_salary * 12;

    -- user
    DBMS_OUTPUT.PUT_LINE('Anual Salary: ' || v_res);

END;

-- with user input
DECLARE
    -- v_salary NUMBER := 3000;
    v_salary NUMBER := &input_salary; -- user input
    v_res NUMBER;
BEGIN

    v_res := v_salary * 12;

    -- user
    DBMS_OUTPUT.PUT_LINE('Anual Salary: ' || v_res);

END;
```
### Exercise 2: Even/Odd Number Checker
Objective: Write a PL/SQL block that checks if a number is even or odd.
```sql

DECLARE
    -- v_salary NUMBER := 3000;
    v_number NUMBER := &input_number; -- user input
    -- v_res NUMBER;
BEGIN

    IF MOD(v_number,2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE('Is an even number');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Is an odd number');
    END IF;

    -- user
    -- DBMS_OUTPUT.PUT_LINE('Anual Salary: ' || v_res);

END;
```
### Exercise 3: Simple Employee Age Check
Objective: Create a block that checks if an employee is eligible for a benefit (must be 18+ years old).
```sql
<>
DECLARE
    -- v_salary NUMBER := 3000;
    -- v_number NUMBER := &input_number; -- user input
    -- v_res NUMBER;
    -- v_age NUMBER := &input_age;
    v_age NUMBER := 16;
    v_res VARCHAR(127);
BEGIN

    /*
    IF MOD(v_number,2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE('Is an even number');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Is an odd number');
    END IF;
    */

    IF v_age > 18 THEN
        v_res := 'You are elegible for a benefit';
    ELSE
        v_res := 'You are NOT elegible for a benefit';
    END IF;

    -- user
    DBMS_OUTPUT.PUT_LINE('You are ' || v_age || ' years old and ' || v_res);

END;
```
