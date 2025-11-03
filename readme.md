https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# ANSWER

# photos
https://quickshare.samsungcloud.com/fzSxXYD12PPw
# chat gpt link
https://chatgpt.com/share/690865b6-e3bc-8009-ad4e-e80d47a7e162

---

# Set-1 — EMPLOYEE (questions 1 and 2)

**Q1 (i, ii, iii):** create `EMPLOYEE`, insert 5 rows; create view `EmployeeView` and give 10% hike to attendance > 95; show average/max/min salary per dept.
**Q2:** PL/SQL program to decrease salary by 10% for employees whose attendance < 70 and show output.

```sql
-- ===== Set-1 =====
-- 1.a Create EMPLOYEE table
CREATE TABLE EMPLOYEE (
  EID NUMBER PRIMARY KEY,
  ENAME VARCHAR2(50),
  DEPT VARCHAR2(20),
  LOCATION VARCHAR2(30),
  SALARY NUMBER(10,2),
  ATTENDANCE_PERCENTAGE NUMBER(5,2)
);

-- 1.b Insert sample rows
INSERT INTO EMPLOYEE VALUES (1, 'Arun',  'CSE', 'Hyderabad', 50000, 96.5);
INSERT INTO EMPLOYEE VALUES (2, 'Bhavana','ECE', 'Vijayawada', 48000, 92.0);
INSERT INTO EMPLOYEE VALUES (3, 'Chaitra','CSE', 'Vizag',     52000, 97.2);
INSERT INTO EMPLOYEE VALUES (4, 'Deepak', 'MECH','Guntur',    45000, 89.5);
INSERT INTO EMPLOYEE VALUES (5, 'Esha',   'CSE', 'Hyderabad', 47000, 99.1);
COMMIT;

-- 1.c Create view of EID, ENAME, DEPT, SALARY
CREATE OR REPLACE VIEW EmployeeView AS
SELECT EID, ENAME, DEPT, SALARY, ATTENDANCE_PERCENTAGE
FROM EMPLOYEE;

-- 1.d Give 10% hike to employees with attendance > 95
UPDATE EMPLOYEE
SET SALARY = SALARY * 1.10
WHERE ATTENDANCE_PERCENTAGE > 95;
COMMIT;

-- Verify the view
SELECT * FROM EmployeeView;

-- 1.e Aggregate: avg, max, min salary per department
SELECT DEPT,
       ROUND(AVG(SALARY),2) AS AVG_SAL,
       MAX(SALARY) AS MAX_SAL,
       MIN(SALARY) AS MIN_SAL
FROM EMPLOYEE
GROUP BY DEPT;

-- 2. PL/SQL: decrease salary by 10% for employees whose attendance < 70
SET SERVEROUTPUT ON;
DECLARE
  CURSOR emp_cur IS
    SELECT EID, SALARY
    FROM EMPLOYEE
    WHERE ATTENDANCE_PERCENTAGE < 70;
BEGIN
  FOR rec IN emp_cur LOOP
    UPDATE EMPLOYEE
    SET SALARY = SALARY - (SALARY * 0.10)
    WHERE EID = rec.EID;
    DBMS_OUTPUT.PUT_LINE('Salary decreased for Employee ID: ' || rec.EID);
  END LOOP;
  COMMIT;
END;
/
```

---

# Set-2 — STUDENT (questions 1 and 2)

**Q1 (i, ii, iii):** create `STUDENT`, insert 5 tuples; create `STUD_VIEW` (ROLLNO, NAME, BRANCH, CGPA) and delete students whose CGPA < 3.0 via view; display average CGPA branch-wise with avg > 7.0.
**Q2:** create `STUDENT_COPY` and trigger to save deleted data.

```sql
-- ===== Set-2 =====
-- 1.a Create STUDENT table
CREATE TABLE STUDENT (
  ROLLNO NUMBER PRIMARY KEY,
  NAME VARCHAR2(30),
  BRANCH VARCHAR2(10),
  SEM NUMBER(2),
  CGPA NUMBER(3,1),
  BACKLOGS NUMBER(2),
  CITY VARCHAR2(20),
  CONTACTNO VARCHAR2(15)
);

-- 1.b Insert sample rows
INSERT INTO STUDENT VALUES (101,'Ravi',  'CSE',5,8.5,0,'Hyderabad','9876543210');
INSERT INTO STUDENT VALUES (102,'Sita',  'ECE',4,7.2,1,'Mumbai',  '8974563210');
INSERT INTO STUDENT VALUES (103,'Arjun', 'EEE',6,2.8,5,'Chennai', '9988776655');
INSERT INTO STUDENT VALUES (104,'Meera', 'CSE',5,6.0,2,'Delhi',   '9911223344');
INSERT INTO STUDENT VALUES (105,'Kiran', 'ECE',4,9.1,0,'Hyderabad','7788996655');
COMMIT;

-- 1.c Create view STUD_VIEW
CREATE OR REPLACE VIEW STUD_VIEW AS
SELECT ROLLNO, NAME, BRANCH, CGPA
FROM STUDENT;

-- Delete students whose CGPA < 3.0 using the view (implements the second subtask)
DELETE FROM STUD_VIEW
WHERE ROLLNO IN (SELECT ROLLNO FROM STUDENT WHERE CGPA < 3.0);
COMMIT;

-- 1.d Display average CGPA branch-wise having avg > 7.0
SELECT BRANCH,
       ROUND(AVG(CGPA),2) AS AVG_CGPA
FROM STUDENT
GROUP BY BRANCH
HAVING AVG(CGPA) > 7.0;

-- 2. Create copy table and delete trigger to store deleted rows
CREATE TABLE STUDENT_COPY AS
SELECT * FROM STUDENT WHERE 1=0; -- empty structure

CREATE OR REPLACE TRIGGER SAVE_DELETED_DATA
AFTER DELETE ON STUDENT
FOR EACH ROW
BEGIN
  INSERT INTO STUDENT_COPY VALUES (
     :OLD.ROLLNO,
     :OLD.NAME,
     :OLD.BRANCH,
     :OLD.SEM,
     :OLD.CGPA,
     :OLD.BACKLOGS,
     :OLD.CITY,
     :OLD.CONTACTNO
  );
END;
/

-- Test trigger (example)
-- DELETE FROM STUDENT WHERE ROLLNO = 103;
-- SELECT * FROM STUDENT_COPY;
```

---

# Set-3 — LIBRARY (questions 1 and 2)

**Q1 (i, ii, iii):** create `LIBRARY` table + 5 inserts; create view `LIB_VIEW` (LIBRARY_NAME, LOCATION, NO_OF_BOOKS, HELPLINE_NO); update KRC Library no_of_books by +550; display libraries having more books than average using nested subquery.
**Q2:** PL/SQL cursor to decrease number of employees by 10% for libraries with more than 25 employees.

```sql
-- ===== Set-3 =====
-- 3.a Create LIBRARY table
CREATE TABLE LIBRARY (
  LIBRARY_NAME VARCHAR2(40) PRIMARY KEY,
  LOCATION VARCHAR2(30),
  NO_OF_BOOKS NUMBER(8),
  NO_OF_EMPLOYEES NUMBER(5),
  LIBRARY_HEAD VARCHAR2(30),
  DATE_OF_ESTABLISHMENT DATE,
  HELPLINE_NO VARCHAR2(15)
);

-- 3.b Insert sample rows
INSERT INTO LIBRARY VALUES ('KRC Library',     'Hyderabad', 42000, 30, 'Mr. Ramesh', TO_DATE('12-02-1998','DD-MM-YYYY'), '1800123456');
INSERT INTO LIBRARY VALUES ('City Central',    'Mumbai',    39000, 22, 'Mrs. Kavita',TO_DATE('05-06-2001','DD-MM-YYYY'), '1800765432');
INSERT INTO LIBRARY VALUES ('Tech Books Hub',  'Bangalore', 45000, 28, 'Mr. Ajay',   TO_DATE('21-09-2010','DD-MM-YYYY'), '1800543210');
INSERT INTO LIBRARY VALUES ('Readers Point',   'Chennai',   25000, 19, 'Mr. Manoj',  TO_DATE('11-11-2005','DD-MM-YYYY'), '1800678912');
INSERT INTO LIBRARY VALUES ('National Library','Delhi',     80000, 40, 'Dr. Meena',  TO_DATE('01-01-1950','DD-MM-YYYY'), '1800987654');
COMMIT;

-- 3.c Create view
CREATE OR REPLACE VIEW LIB_VIEW AS
SELECT LIBRARY_NAME, LOCATION, NO_OF_BOOKS, HELPLINE_NO
FROM LIBRARY;

-- Update KRC Library number of books (add 550)
UPDATE LIB_VIEW
SET NO_OF_BOOKS = NO_OF_BOOKS + 550
WHERE LIBRARY_NAME = 'KRC Library';
COMMIT;

-- 3.iii Display libraries having more books than average across all libraries (nested subquery)
SELECT LIBRARY_NAME, LOCATION, NO_OF_BOOKS
FROM LIBRARY
WHERE NO_OF_BOOKS > (SELECT AVG(NO_OF_BOOKS) FROM LIBRARY);

-- 3.2 PL/SQL: decrease number of employees by 10% for libraries with > 25 employees
SET SERVEROUTPUT ON;
DECLARE
  CURSOR emp_cur IS
    SELECT LIBRARY_NAME, NO_OF_EMPLOYEES
    FROM LIBRARY
    WHERE NO_OF_EMPLOYEES > 25;
BEGIN
  FOR rec IN emp_cur LOOP
    UPDATE LIBRARY
    SET NO_OF_EMPLOYEES = NO_OF_EMPLOYEES - ROUND(NO_OF_EMPLOYEES * 0.10)
    WHERE LIBRARY_NAME = rec.LIBRARY_NAME;
    DBMS_OUTPUT.PUT_LINE('Employees updated for: ' || rec.LIBRARY_NAME);
  END LOOP;
  COMMIT;
END;
/
```

---

# Set-4 — PURCHASE (questions 1 and 2)

**Q1 (i, ii, iii):** create `PURCHASE` + 5 inserts; create `Purchase_View` (OrderID, Item_Name, Final_Cost, Warranty_Period) ordered by cost; show aggregate functions total items, average cost, highest & lowest final cost.
**Q2:** trigger: prevent negative OrderID using `BEFORE INSERT OR UPDATE` with `RAISE_APPLICATION_ERROR`.

```sql
-- ===== Set-4 =====
-- 4.a Create PURCHASE table
CREATE TABLE PURCHASE (
  OrderID NUMBER PRIMARY KEY,
  DateOfPurchase DATE,
  Item_Name VARCHAR2(50),
  Original_Cost NUMBER(10,2),
  Discount NUMBER(10,2),
  Final_Cost NUMBER(10,2),
  Warranty_Period NUMBER, -- months
  Item_Weight NUMBER(5,2)
);

-- 4.b Insert 5 tuples
INSERT INTO PURCHASE VALUES (101, TO_DATE('15-JAN-2025','DD-MON-YYYY'), 'Laptop',     55000, 5000, 50000, 24, 2.5);
INSERT INTO PURCHASE VALUES (102, TO_DATE('08-FEB-2025','DD-MON-YYYY'), 'Smartphone', 30000, 2000, 28000, 12, 0.25);
INSERT INTO PURCHASE VALUES (103, TO_DATE('14-FEB-2025','DD-MON-YYYY'), 'Smartwatch', 8000, 1000, 7000,  6, 0.10);
INSERT INTO PURCHASE VALUES (104, TO_DATE('01-MAR-2025','DD-MON-YYYY'), 'Headphones', 2000, 200,  1800,  3, 0.15);
INSERT INTO PURCHASE VALUES (105, TO_DATE('10-MAR-2025','DD-MON-YYYY'), 'Tablet',     22000, 3000, 19000, 18, 0.50);
COMMIT;

-- 4.c Create view and order by Final_Cost
CREATE OR REPLACE VIEW Purchase_View AS
SELECT OrderID, Item_Name, Final_Cost, Warranty_Period
FROM PURCHASE
ORDER BY Final_Cost;

-- See the view
SELECT * FROM Purchase_View;

-- 4.d Aggregate functions: total items, average cost, highest and lowest final cost
SELECT COUNT(*) AS Total_Items,
       ROUND(AVG(Final_Cost),2) AS Average_Cost,
       MAX(Final_Cost) AS Highest_Cost,
       MIN(Final_Cost) AS Lowest_Cost
FROM PURCHASE;

-- 4.2 Trigger to prevent negative OrderID (BEFORE INSERT OR UPDATE)
CREATE OR REPLACE TRIGGER Check_OrderID
BEFORE INSERT OR UPDATE ON PURCHASE
FOR EACH ROW
BEGIN
  IF :NEW.OrderID < 0 THEN
    RAISE_APPLICATION_ERROR(-20001, 'OrderID cannot be negative!');
  END IF;
END;
/

-- Test the trigger (example)
-- INSERT INTO PURCHASE VALUES (-201, TO_DATE('20-MAR-2025','DD-MON-YYYY'), 'Camera', 25000,3000,22000,12,0.8);
-- The above should raise an error and be prevented.
```

---

# Set-5 — CUSTOMER & ORDERS (questions 1 and 2)

**Q1 (i, ii, iii):** create `CUSTOMER` and `ORDERS` (with FK), insert data; demonstrate joins: inner join for customers who placed orders, left join for customers with no orders, orders without corresponding customers; create `HIGH_VALUE_ORDERS` view for amount > 1000.
**Q2:** apply a trigger on `ORDERS` that inserts deleted rows into `ORDERS_BACKUP`.

```sql
-- ===== Set-5 =====
-- 5.a Create CUSTOMER and ORDERS tables
CREATE TABLE CUSTOMER (
  CID NUMBER PRIMARY KEY,
  CNAME VARCHAR2(30),
  CITY VARCHAR2(20),
  CONTACT_NO VARCHAR2(15)
);

CREATE TABLE ORDERS (
  OID NUMBER PRIMARY KEY,
  CID NUMBER,
  ORDER_DATE DATE,
  ITEM VARCHAR2(30),
  AMOUNT NUMBER(10),
  CONSTRAINT fk_customer FOREIGN KEY (CID) REFERENCES CUSTOMER(CID)
);

-- 5.b Insert CUSTOMER values
INSERT INTO CUSTOMER VALUES (101,'Ravi','Hyderabad','9876543210');
INSERT INTO CUSTOMER VALUES (102,'Sita','Mumbai',   '9998776655');
INSERT INTO CUSTOMER VALUES (103,'Arjun','Chennai', '7896541230');
INSERT INTO CUSTOMER VALUES (104,'Meera','Delhi',   '8899776655');
COMMIT;

-- 5.c Insert ORDER values (note: OID values must be unique and CID must match existing or be NULL)
INSERT INTO ORDERS VALUES (201,101, TO_DATE('10-10-2024','DD-MM-YYYY'), 'Laptop', 55000);
INSERT INTO ORDERS VALUES (202,101, TO_DATE('15-10-2024','DD-MM-YYYY'), 'Bag',     900);
INSERT INTO ORDERS VALUES (203,102, TO_DATE('09-09-2024','DD-MM-YYYY'), 'Phone', 25000);
INSERT INTO ORDERS VALUES (204,NULL, TO_DATE('11-08-2024','DD-MM-YYYY'), 'Book',    500); -- order with no matching customer
COMMIT;

-- 5.ii Joins:
-- Customers who placed orders (inner join)
SELECT C.CID, C.CNAME, O.OID, O.ITEM, O.AMOUNT
FROM CUSTOMER C
INNER JOIN ORDERS O ON C.CID = O.CID;

-- Customers who have not placed orders (left join + null check)
SELECT C.CID, C.CNAME
FROM CUSTOMER C
LEFT JOIN ORDERS O ON C.CID = O.CID
WHERE O.CID IS NULL;

-- Orders without matching customers (orders with no corresponding customer)
SELECT O.OID, O.ITEM, O.AMOUNT
FROM ORDERS O
LEFT JOIN CUSTOMER C ON O.CID = C.CID
WHERE C.CID IS NULL;

-- 5.iii Create a view of ORDERS where AMOUNT > 1000
CREATE OR REPLACE VIEW HIGH_VALUE_ORDERS AS
SELECT OID, ORDER_DATE, AMOUNT
FROM ORDERS
WHERE AMOUNT > 1000;

-- To display
SELECT * FROM HIGH_VALUE_ORDERS;

-- 5.2 Trigger on ORDERS for DELETE: Save deleted rows into ORDERS_BACKUP
CREATE TABLE ORDERS_BACKUP AS SELECT * FROM ORDERS WHERE 1=0;

CREATE OR REPLACE TRIGGER ORDER_DELETE_BACKUP
AFTER DELETE ON ORDERS
FOR EACH ROW
BEGIN
  INSERT INTO ORDERS_BACKUP VALUES (
    :OLD.OID,
    :OLD.CID,
    :OLD.ORDER_DATE,
    :OLD.ITEM,
    :OLD.AMOUNT
  );
END;
/

-- Test trigger (example)
-- DELETE FROM ORDERS WHERE OID = 202;
-- SELECT * FROM ORDERS_BACKUP;
```

---





# END
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
