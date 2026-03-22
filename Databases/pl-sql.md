# PL/SQL
Bu fayl PL/SQL bo'yicha amaliy misollarni tartibli ko'rinishda jamlaydi.

- [PL/SQL](#plsql-cheat-sheet-cp)
  - [1) Kichik misollar](#1-kichik-misollar)
  - [2) Procedure va Function](#2-procedure-va-function)
  - [3) Cursor](#3-cursor)
  - [4) Records](#4-records)
  - [5) Exception](#5-exception)
  - [6) Triggers](#6-triggers)
  - [7) Collections](#7-collections)
  - [8) Transactions](#8-transactions)

## 1) Kichik misollar

Ikki sonni qo'shish:

```sql
DECLARE
  a NUMBER := 5;
  b NUMBER;
  c NUMBER;
BEGIN
  b := 10;
  c := a + b;
  DBMS_OUTPUT.PUT_LINE(c);
END;
```

Jadvaldan ma'lumot o'qish:

```sql
DECLARE
  s_id   students.student_id%TYPE := 3;
  s_name students.fio%TYPE;
  s_phone students.phone_number%TYPE;
  s_addr students.address%TYPE;
BEGIN
  SELECT fio, phone_number, address
  INTO s_name, s_phone, s_addr
  FROM students
  WHERE student_id = s_id;

  DBMS_OUTPUT.PUT_LINE('Name ' || s_name || ' from ' || s_addr || ' phone ' || s_phone);
END;
```

`IF` bilan taqqoslash:

```sql
DECLARE
  a NUMBER := 11;
  b NUMBER := 15;
BEGIN
  IF a > b THEN
    DBMS_OUTPUT.PUT_LINE('a soni katta');
  ELSIF a < b THEN
    DBMS_OUTPUT.PUT_LINE('b soni katta');
  ELSE
    DBMS_OUTPUT.PUT_LINE('sonlar teng');
  END IF;
END;
```

`NULL` tekshirish:

```sql
DECLARE
  a NUMBER;
  b NUMBER := 10;
BEGIN
  IF a IS NULL THEN
    DBMS_OUTPUT.PUT_LINE('null qiymatga ega');
  END IF;
END;
```

Lokal protsedura bilan ishlash:

```sql
DECLARE
  PROCEDURE compare(a NUMBER, b NUMBER) IS
  BEGIN
    IF a > b THEN
      DBMS_OUTPUT.PUT_LINE('A > B');
    ELSE
      DBMS_OUTPUT.PUT_LINE('A < B');
    END IF;
  END;
BEGIN
  compare(10, 20);
  compare(12, 5);
END;
```

`CASE` bilan ishlash:

```sql
DECLARE
  grade CHAR(1) := '5';
BEGIN
  CASE grade
    WHEN '5' THEN DBMS_OUTPUT.PUT_LINE('Excellent');
    WHEN '4' THEN DBMS_OUTPUT.PUT_LINE('Very good');
    WHEN '3' THEN DBMS_OUTPUT.PUT_LINE('Well done');
    ELSE DBMS_OUTPUT.PUT_LINE('No such grade');
  END CASE;
END;
```

`LOOP` bilan ishlash:

```sql
DECLARE
  x NUMBER := 0;
BEGIN
  LOOP
    DBMS_OUTPUT.PUT_LINE(x);
    x := x + 1;
    EXIT WHEN x > 10;
  END LOOP;
END;
```

`FOR .. IN ..` bilan ishlash:

```sql
BEGIN
  FOR a IN 1 .. 10 LOOP
    DBMS_OUTPUT.PUT_LINE('a: ' || a);
  END LOOP;
END;
```

`WHILE` bilan ishlash:

```sql
DECLARE
  a NUMBER := 0;
BEGIN
  WHILE a < 10 LOOP
    DBMS_OUTPUT.PUT_LINE('a: ' || a);
    a := a + 1;
  END LOOP;
END;
```

String funksiyalari:

```sql
DECLARE
  greetings VARCHAR2(11) := 'salom dunyo';
BEGIN
  DBMS_OUTPUT.PUT_LINE(UPPER(greetings));
  DBMS_OUTPUT.PUT_LINE(LOWER(greetings));
  DBMS_OUTPUT.PUT_LINE(INITCAP(greetings));
  DBMS_OUTPUT.PUT_LINE(SUBSTR(greetings, 1, 3));
  DBMS_OUTPUT.PUT_LINE(SUBSTR(greetings, -1, 1));
  DBMS_OUTPUT.PUT_LINE(SUBSTR(greetings, 7, 5));
  DBMS_OUTPUT.PUT_LINE(SUBSTR(greetings, 2));
END;
```

VARRAY bilan ishlash:

```sql
DECLARE
  TYPE names_array IS VARRAY(5) OF VARCHAR2(100);
  names names_array;
  total INTEGER;
BEGIN
  names := names_array('Aziz', 'Qodir', 'Karim', 'Botir');
  total := names.COUNT;
  DBMS_OUTPUT.PUT_LINE('Total ' || total || ' Students');

  FOR i IN 1 .. total LOOP
    DBMS_OUTPUT.PUT_LINE('Student: ' || names(i));
  END LOOP;
END;
```

Cursor + type + array bilan ishlash:

```sql
DECLARE
  CURSOR c_students IS
    SELECT fio FROM students;

  TYPE c_list IS VARRAY(100) OF students.fio%TYPE;
  name_list c_list := c_list();
  counter INTEGER := 0;
BEGIN
  FOR n IN c_students LOOP
    counter := counter + 1;
    name_list.EXTEND;
    name_list(counter) := n.fio;
    DBMS_OUTPUT.PUT_LINE('Talaba(' || counter || '): ' || name_list(counter));
  END LOOP;
END;
```

## 2) Procedure va Function

`Hello world` protsedurasi:

```sql
CREATE OR REPLACE PROCEDURE salom
AS
BEGIN
  DBMS_OUTPUT.PUT_LINE('Hello world');
END;
/

BEGIN
  salom;
END;
/
```

Ikki sonni qo'shish (`IN`, `OUT`):

```sql
DECLARE
  a NUMBER;
  b NUMBER;
  c NUMBER;

  PROCEDURE summa(x IN NUMBER, y IN NUMBER, z OUT NUMBER) IS
  BEGIN
    z := x + y;
  END;
BEGIN
  a := 8;
  b := 5;
  summa(a, b, c);
  DBMS_OUTPUT.PUT_LINE('a + b = ' || c);
END;
/
```

Protsedurani o'chirish:

```sql
DROP PROCEDURE summa;
```

`IN OUT` bilan kvadrat hisoblash:

```sql
DECLARE
  a NUMBER := 5;

  PROCEDURE square_num(x IN OUT NUMBER) IS
  BEGIN
    x := x * x;
  END;
BEGIN
  square_num(a);
  DBMS_OUTPUT.PUT_LINE('(5) ni kvadrati: ' || a);
END;
/
```

Funksiya yaratish va chaqirish:

```sql
CREATE OR REPLACE FUNCTION total_students
RETURN NUMBER
IS
  total NUMBER(10) := 0;
BEGIN
  SELECT COUNT(*) INTO total
  FROM students;
  RETURN total;
END;
/

DECLARE
  c NUMBER(10);
BEGIN
  c := total_students();
  DBMS_OUTPUT.PUT_LINE('Soni: ' || c);
END;
/
```

Lokal funksiya bilan ishlash:

```sql
DECLARE
  a NUMBER;
  b NUMBER;
  c NUMBER;

  FUNCTION find_max(x IN NUMBER, y IN NUMBER)
  RETURN NUMBER
  IS
    z NUMBER;
  BEGIN
    IF x > y THEN
      z := x;
    ELSE
      z := y;
    END IF;
    RETURN z;
  END;
BEGIN
  a := 10;
  b := 8;
  c := find_max(a, b);
  DBMS_OUTPUT.PUT_LINE('kattasi: ' || c);
END;
/
```

## 3) Cursor

`SQL%FOUND` va `SQL%NOTFOUND` bilan ishlash:

```sql
DECLARE
  total_rows NUMBER(10);
BEGIN
  UPDATE students
  SET phone_number = phone_number + 500;

  IF SQL%NOTFOUND THEN
    DBMS_OUTPUT.PUT_LINE('Qator topilmadi');
  ELSIF SQL%FOUND THEN
    total_rows := SQL%ROWCOUNT;
    DBMS_OUTPUT.PUT_LINE(total_rows || ' qator yangilandi');
  END IF;
END;
/
```

Oddiy cursor:

```sql
DECLARE
  c_id   students.student_id%TYPE;
  c_fio  students.fio%TYPE;
  c_date students.birth_date%TYPE;

  CURSOR c_students IS
    SELECT student_id, fio, birth_date
    FROM students;
BEGIN
  OPEN c_students;
  LOOP
    FETCH c_students INTO c_id, c_fio, c_date;
    EXIT WHEN c_students%NOTFOUND;
    DBMS_OUTPUT.PUT_LINE(c_id || ' ' || c_fio || ' ' || c_date);
  END LOOP;
  CLOSE c_students;
END;
/
```

## 4) Records

`%ROWTYPE` orqali bitta qatorni olish:

```sql
DECLARE
  student_rec students%ROWTYPE;
BEGIN
  SELECT *
  INTO student_rec
  FROM students
  WHERE student_id = 4;

  DBMS_OUTPUT.PUT_LINE('Student ID: ' || student_rec.student_id);
  DBMS_OUTPUT.PUT_LINE('Student FIO: ' || student_rec.fio);
  DBMS_OUTPUT.PUT_LINE('Student phone number: ' || student_rec.phone_number);
  DBMS_OUTPUT.PUT_LINE('Student address: ' || student_rec.address);
END;
/
```

Cursor orqali `record` bilan ishlash:

```sql
DECLARE
  CURSOR student_cur IS
    SELECT student_id, fio, address
    FROM students;

  student_rec student_cur%ROWTYPE;
BEGIN
  OPEN student_cur;
  LOOP
    FETCH student_cur INTO student_rec;
    EXIT WHEN student_cur%NOTFOUND;
    DBMS_OUTPUT.PUT_LINE(student_rec.student_id || ' ' || student_rec.fio);
  END LOOP;
  CLOSE student_cur;
END;
/
```

## 5) Exception

Exception bilan ishlash:

```sql
DECLARE
  c_id   students.student_id%TYPE := 3;
  c_name students.fio%TYPE;
  c_addr students.address%TYPE;
BEGIN
  SELECT fio, address
  INTO c_name, c_addr
  FROM students
  WHERE student_id = c_id;

  DBMS_OUTPUT.PUT_LINE('Name: ' || c_name);
  DBMS_OUTPUT.PUT_LINE('Address: ' || c_addr);
EXCEPTION
  WHEN NO_DATA_FOUND THEN
    DBMS_OUTPUT.PUT_LINE('No such student');
  WHEN OTHERS THEN
    DBMS_OUTPUT.PUT_LINE('Error!');
END;
/
```

## 6) Triggers

Insert/Update/Delete uchun trigger:

```sql
CREATE OR REPLACE TRIGGER display_fortest_changes
BEFORE INSERT OR UPDATE OR DELETE ON fortest
FOR EACH ROW
BEGIN
  IF INSERTING THEN
    DBMS_OUTPUT.PUT_LINE('New name: ' || :NEW.name);
  ELSIF UPDATING THEN
    DBMS_OUTPUT.PUT_LINE('Old name: ' || :OLD.name);
    DBMS_OUTPUT.PUT_LINE('New name: ' || :NEW.name);
  ELSIF DELETING THEN
    DBMS_OUTPUT.PUT_LINE('Old name: ' || :OLD.name);
  END IF;
END;
/
```

Trigger bo'yicha amallar:

```sql
DROP TRIGGER display_fortest_changes;

INSERT INTO fortest VALUES (1, '1-ustun');
INSERT INTO fortest VALUES (2, '2-ustun');
INSERT INTO fortest VALUES (3, '3-ustun');
INSERT INTO fortest VALUES (4, '4-ustun');

UPDATE fortest
SET name = '44-ustun'
WHERE id = 4;

DELETE FROM fortest WHERE id = 1;
SELECT * FROM fortest;
```

## 7) Collections

Associative array (`INDEX BY`) bilan ishlash:

```sql
DECLARE
  TYPE names IS TABLE OF NUMBER INDEX BY VARCHAR2(20);
  name_list names;
  name VARCHAR2(20);
BEGIN
  name_list('Aziz') := 62000;
  name_list('Umar') := 75000;
  name_list('Doston') := 100000;
  name_list('Odil') := 78000;

  name := name_list.FIRST;
  WHILE name IS NOT NULL LOOP
    DBMS_OUTPUT.PUT_LINE('Name of ' || name || ' is ' || TO_CHAR(name_list(name)));
    name := name_list.NEXT(name);
  END LOOP;
END;
/
```

## 8) Transactions

`SAVEPOINT` va `ROLLBACK` bilan ishlash:

```sql
DELETE FROM fortest;

INSERT INTO fortest (id, name) VALUES (1, 'Aziz');
INSERT INTO fortest (id, name) VALUES (2, 'Umar');

SAVEPOINT savetoday;

INSERT INTO fortest (id, name) VALUES (3, 'Doston');

ROLLBACK TO savetoday;
COMMIT;

SELECT * FROM fortest;
```
