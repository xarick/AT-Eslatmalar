# SQL

Bu fayl SQL asoslarini tez ishlatish uchun qisqa va amaliy qo'llanma.

## 0) Qisqa nazariya

Ma'lumotlar bazasi modellari:
- Ierarxik (daraxtsimon) model
- Tarmoqli (o'zaro bog'langan) model
- Relyatsion (jadvallar ko'rinishida) model

SQL komponentlari:
- `DDL`: `CREATE`, `ALTER`, `DROP`, `TRUNCATE`
- `DML`: `SELECT`, `INSERT`, `UPDATE`, `DELETE`
- `TCL`: `COMMIT`, `ROLLBACK`, `SAVEPOINT`
- `DCL`: `GRANT`, `REVOKE`

## 1) Konsolga kirish

```bash
mysql -u root -p                    # MySQL konsoliga kirish uchun
psql -U postgres                    # PostgreSQL konsoliga kirish uchun
psql -U postgres -d mydatabase      # Tanlangan bazaga ulanib kirish uchun
```

## 2) Baza va jadval bilan ishlash (DDL)

```sql
SHOW DATABASES;                     -- Bazalar ro'yxatini ko'rish uchun (MySQL)
CREATE DATABASE some_db;            -- Yangi baza yaratish uchun
CREATE DATABASE some_db
  DEFAULT CHARACTER SET utf8mb4;    -- Kodirovka bilan baza yaratish uchun
DROP DATABASE some_db;              -- Bazani o'chirish uchun

USE some_db;                        -- Bazani tanlash uchun (MySQL)
SHOW TABLES;                        -- Jadval ro'yxatini ko'rish uchun (MySQL)
DESCRIBE students;                  -- Jadval ustunlarini ko'rish uchun (MySQL)

CREATE TABLE students (
  id INT PRIMARY KEY,
  full_name VARCHAR(255),
  birth_date DATE,
  address VARCHAR(255),
  group_id INT
);                                  -- Jadval yaratish uchun

CREATE TABLE all_groups (
  id INT PRIMARY KEY,
  name VARCHAR(255),
  teacher_id INT
);                                  -- Guruhlar jadvalini yaratish uchun

CREATE TABLE teachers (
  id INT PRIMARY KEY,
  full_name VARCHAR(255)
);                                  -- O'qituvchilar jadvalini yaratish uchun
```

## 3) Ma'lumot qo'shish (INSERT)

```sql
INSERT INTO students (id, full_name, birth_date, address, group_id)
VALUES
  (1, 'Umarov Aziz', '1997-07-17', 'Andijon', 1),
  (2, 'Botir Toxirov', '1994-05-10', 'Toshkent', 1),
  (3, 'Umarov Aziz', '1995-05-13', 'Samarqand', 2),
  (4, 'Umarov Karim', '1995-02-26', 'Buxoro', 2);  -- Talabalarni qo'shish uchun

INSERT INTO teachers (id, full_name)
VALUES
  (1, 'Olimova Feruza'),
  (2, 'Kamolov Aziz'),
  (3, 'Qodirov Azamat');            -- O'qituvchilarni qo'shish uchun

INSERT INTO all_groups (id, name, teacher_id)
VALUES
  (1, '100', 2),
  (2, '101', 1),
  (3, '102', 3);                    -- Guruhlarni qo'shish uchun
```

## 4) SELECT asoslari

```sql
SELECT * FROM students;                                 -- Barcha ustunlarni ko'rish uchun
SELECT full_name, birth_date, address FROM students;    -- Tanlangan ustunlarni ko'rish uchun
SELECT full_name AS fio, address AS manzil FROM students; -- Ustunga alias berish uchun

SELECT MIN(id) FROM students;                           -- Eng kichik qiymatni olish uchun
SELECT MAX(id) FROM students;                           -- Eng katta qiymatni olish uchun
SELECT COUNT(*) FROM students;                          -- Qatorlar sonini olish uchun
SELECT AVG(id) FROM students;                           -- O'rtacha qiymatni olish uchun
SELECT SUM(id) FROM students;                           -- Yig'indini olish uchun

SELECT UPPER(full_name) FROM students;                  -- Matnni katta harfda ko'rish uchun
SELECT LOWER(full_name) FROM students;                  -- Matnni kichik harfda ko'rish uchun
SELECT LENGTH(full_name) FROM students;                 -- Matn uzunligini ko'rish uchun
SELECT CONCAT(full_name, ', ', address) AS fio_manzil
FROM students;                                          -- Ustunlarni birlashtirib ko'rish uchun
```

## 5) Filtrlash, saralash va guruhlash

```sql
SELECT * FROM students WHERE address = 'Andijon';       -- Bitta shart bo'yicha filtrlash uchun
SELECT * FROM students WHERE group_id = 1;              -- group_id bo'yicha filtrlash uchun
SELECT * FROM students WHERE address = 'Andijon' AND group_id = 1; -- Bir nechta shart uchun

SELECT * FROM students WHERE full_name LIKE 'Um%';      -- Boshlanishiga ko'ra qidirish uchun
SELECT * FROM students WHERE full_name LIKE '%aziz%';   -- Ichida bor qiymat bo'yicha qidirish uchun
SELECT * FROM students WHERE address LIKE '_ndijon';    -- Bitta belgili pattern bilan qidirish uchun

SELECT * FROM students WHERE address IN ('Andijon', 'Samarqand');  -- IN bo'yicha filtrlash uchun
SELECT * FROM students WHERE address NOT IN ('Andijon', 'Samarqand'); -- NOT IN uchun
SELECT * FROM students WHERE address IS NULL;           -- NULL qiymatlarni ko'rish uchun
SELECT * FROM students WHERE address IS NOT NULL;       -- NULL bo'lmagan qiymatlar uchun

SELECT * FROM students
WHERE (address = 'Andijon' OR address = 'Toshkent') AND group_id = 1; -- Murakkab shart uchun

SELECT * FROM students WHERE id > 2;                    -- Taqqoslash bo'yicha filtrlash uchun
SELECT * FROM students WHERE id > 2 AND id <= 5;        -- Oraliq shart bilan filtrlash uchun
SELECT * FROM students WHERE id BETWEEN 2 AND 4;        -- BETWEEN bo'yicha filtrlash uchun
SELECT * FROM students WHERE id BETWEEN 2 AND 4 AND group_id = 2; -- Qo'shimcha shart uchun

SELECT * FROM students ORDER BY id;                     -- O'sish tartibida saralash uchun
SELECT * FROM students ORDER BY id DESC;                -- Kamayish tartibida saralash uchun
SELECT * FROM students ORDER BY id DESC LIMIT 2;        -- Cheklangan natijani olish uchun

SELECT group_id, COUNT(address)
FROM students
GROUP BY group_id;                                      -- Guruhlab hisoblash uchun

SELECT DISTINCT group_id FROM students;                 -- Takrorlanmas qiymatlarni ko'rish uchun
SELECT COUNT(DISTINCT group_id) AS groups_count
FROM students;                                          -- Takrorlanmas sonni hisoblash uchun
```

## 6) Subquery

```sql
SELECT * FROM students
WHERE id = (SELECT MAX(id) FROM students);              -- Ichki so'rov natijasi bo'yicha filtrlash uchun
```

## 6.1) SELECT ketma-ketligi

```sql
SELECT *
FROM students
WHERE group_id = 1
GROUP BY group_id
ORDER BY group_id
LIMIT 5;
```

## 7) JOIN bilan ishlash

JOIN diagrammalari:
- [1-rasm](./images/joins_1.png)
- [2-rasm](./images/joins_2.png)

```sql
SELECT *
FROM students s
INNER JOIN all_groups g ON s.group_id = g.id;           -- Mos qatorlarni olish uchun

SELECT *
FROM students s
LEFT JOIN all_groups g ON s.group_id = g.id;            -- Chap jadvalni to'liq olish uchun

SELECT *
FROM students s
RIGHT JOIN all_groups g ON s.group_id = g.id;           -- O'ng jadvalni to'liq olish uchun

SELECT
  s.full_name AS fio,
  s.birth_date AS sana,
  s.address AS manzil,
  g.name AS guruh
FROM students s
JOIN all_groups g ON s.group_id = g.id
WHERE g.teacher_id = 2;                                 -- JOIN natijasini filtrlash uchun
```

SELF JOIN misoli:

```sql
SELECT
  s1.full_name AS student_name,
  s2.full_name AS mentor_name
FROM students s1
JOIN students s2 ON s1.group_id = s2.group_id
WHERE s1.id <> s2.id;                                   -- Bir jadvalni o'ziga bog'lash uchun
```

MySQL'da `FULL OUTER JOIN` uchun `UNION` usuli:

```sql
SELECT *
FROM students s
LEFT JOIN all_groups g ON s.group_id = g.id
UNION
SELECT *
FROM students s
RIGHT JOIN all_groups g ON s.group_id = g.id;
```

## 8) Jadvalni o'zgartirish (ALTER)

```sql
CREATE TABLE jobs (
  id INT,
  name VARCHAR(255)
);                                  -- Namuna jadval yaratish uchun

DESCRIBE jobs;                      -- Ustunlarni ko'rish uchun (MySQL)
ALTER TABLE jobs ADD address VARCHAR(255);              -- Ustun qo'shish uchun
ALTER TABLE jobs DROP COLUMN address;                   -- Ustunni olib tashlash uchun
ALTER TABLE jobs RENAME COLUMN address TO addr;         -- Ustun nomini o'zgartirish uchun
ALTER TABLE jobs MODIFY COLUMN addr VARCHAR(100);       -- Ustun tipini o'zgartirish uchun (MySQL)

DROP TABLE jobs;                    -- Jadvalni o'chirish uchun
```
