
# 📦 Backup and Recovery in Databases

## 🔄 1. Backup Strategies

Backups are essential to ensure that data is not lost due to system failure, corruption, or accidental deletion.

### ✅ Types of Backups:

#### a) Full Backup
- Backs up the entire database.
- Example:
```sql
-- MySQL
mysqldump -u root -p mydatabase > full_backup.sql
```

#### b) Incremental Backup
- Backs up data changed since the last backup.
- Requires less storage.
- Typically done using backup tools with timestamp tracking.

#### c) Differential Backup
- Backs up data changed since the last full backup.
- Takes more space than incremental but faster recovery.

---

## ♻️ 2. Restoring Databases

To restore a database means to bring it back to a previous state using a backup.

### ✅ Example:
```bash
mysql -u root -p mydatabase < full_backup.sql
```

### 🛠 Restore Strategy:
1. Identify the latest full backup.
2. Apply the latest differential or incremental backups in order.
3. Ensure database is in consistent state.

---

## ✅ 3. Ensuring Data Integrity and Consistency

Ensures that the data in your database is:

- Accurate (correct values)

- Consistent (no contradictions)

- Reliable (doesn’t get corrupted)

##   Ways to Ensure Data Integrity

`🔸 a. Constraints (like PRIMARY KEY, FOREIGN KEY, CHECK, NOT NULL)`
```mysql
CREATE TABLE Students (
  StudentID INT PRIMARY KEY,
  Name VARCHAR(50) NOT NULL,
  Age INT CHECK (Age > 0)
);

```
`🔸 b. Transactions (BEGIN, COMMIT, ROLLBACK)`

To ensure atomic operations — either everything happens or nothing.


```mysql
START TRANSACTION;

UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;

COMMIT;

```
` 🔹 If something fails in between, use:`

```sql
ROLLBACK;

```
`🔸 c. ACID Properties`

| Property    | Meaning                              |
| ----------- | ------------------------------------ |
| Atomicity   | All or nothing                       |
| Consistency | Data must be valid                   |
| Isolation   | Transactions don’t affect each other |
| Durability  | Once committed, changes stay         |



## Output Example (Demo)
Let’s say you backed up a students table:

```sql

-- Restore:
mysql -u root -p school < backup_students.sql
```

`Then verify:`

```sql

SELECT * FROM students;
```

`✅ You’ll see the data back in place — just like before crash.`

## 💡 Best Practices:

- Automate regular backups (daily/weekly).
- Store backups securely (offsite or in the cloud).
- Test backups by restoring them periodically.
- Use database tools like MySQL Workbench, pgAdmin, or automated services.
