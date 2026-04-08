# 🏥 Hospital Management System — SQL Project

A complete, beginner-to-advanced SQL project built on a real-world Hospital Management domain.  
Covers schema design, sample data, JOINs, subqueries, window functions, views, stored procedures, and 10 interview questions — all in one runnable file.

---

## 📌 Project Overview

| Item | Details |
|---|---|
| **Domain** | Healthcare / Hospital Management |
| **Database** | MySQL 8+ / PostgreSQL 13+ |
| **Tables** | 11 tables |
| **Sample Rows** | 50+ realistic rows |
| **Queries** | 35+ queries across 10 phases |
| **Skill Level** | Intermediate → Advanced |

---

## 🗂️ Database Schema

```
departments
    └── doctors          (many doctors per department)
    └── nurses           (many nurses per department)
    └── rooms            (many rooms per department)

patients
    └── appointments     (patient ↔ doctor)
    └── medical_records  (patient ↔ doctor)
        └── prescriptions (record ↔ medication)
    └── room_assignments (patient ↔ room)
    └── billing          (linked to appointment)

medications              (standalone lookup table)
```

### Tables at a glance

| Table | Description |
|---|---|
| `departments` | Hospital departments (Cardiology, Neurology, etc.) |
| `doctors` | Doctor profiles with specialization and salary |
| `patients` | Patient demographics and contact info |
| `nurses` | Nurse records with shift info |
| `rooms` | Room types, availability, and pricing |
| `appointments` | Patient-doctor appointment scheduling |
| `medical_records` | Diagnosis and treatment records |
| `medications` | Medication catalog with stock |
| `prescriptions` | Medications prescribed per visit |
| `room_assignments` | Patient admission and discharge tracking |
| `billing` | Bill breakdown and payment status |

---

## 📚 What You Will Learn

| Phase | Topic | Concepts Covered |
|---|---|---|
| 1 | Schema Design | `CREATE TABLE`, Primary Keys, Foreign Keys, `ENUM`, `DEFAULT` |
| 2 | Sample Data | `INSERT INTO`, realistic data |
| 3 | Basic Queries | `SELECT`, `WHERE`, `ORDER BY`, `LIKE`, `BETWEEN` |
| 4 | JOINs | `INNER JOIN`, `LEFT JOIN`, multi-table joins |
| 5 | Subqueries | `IN`, correlated subqueries, `EXISTS` |
| 6 | Aggregations | `GROUP BY`, `HAVING`, `COUNT`, `SUM`, `AVG`, `MAX`, `MIN` |
| 7 | Window Functions | `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()`, `LAG()`, running totals |
| 8 | Views | `CREATE VIEW`, reusable query logic |
| 9 | Stored Procedures | `CREATE PROCEDURE`, `CALL`, multi-result procedures |
| 10 | Indexes & Interview | `CREATE INDEX`, 10 interview Q&As with answers |

---

## 🚀 How to Run

### Option 1 — MySQL Workbench (Recommended for beginners)

1. Open **MySQL Workbench** and connect to your local server
2. Create a new database:
   ```sql
   CREATE DATABASE hospital_db;
   USE hospital_db;
   ```
3. Go to **File → Open SQL Script** and select `hospital_management_project.sql`
4. Click the ⚡ **Execute** button (or press `Ctrl + Shift + Enter`)
5. All tables, data, and queries will run top to bottom ✅

### Option 2 — Command Line

```bash
mysql -u root -p
```
```sql
CREATE DATABASE hospital_db;
USE hospital_db;
SOURCE /path/to/hospital_management_project.sql;
```

### Option 3 — VS Code with SQLTools Extension

1. Install the **SQLTools** extension in VS Code
2. Connect to your MySQL server
3. Open the `.sql` file and run it

---

## 📂 File Structure

```
hospital-sql-project/
│
├── hospital_management_project.sql   ← Main project file (run this)
└── README.md                         ← This file
```

---

## 💡 Sample Queries Preview

**Find patients with pending bills who visited more than once:**
```sql
SELECT
    CONCAT(p.first_name, ' ', p.last_name) AS patient_name,
    COUNT(a.appointment_id) AS total_visits,
    b.payment_status
FROM patients p
JOIN appointments a ON p.patient_id = a.patient_id
JOIN billing      b ON p.patient_id = b.patient_id
WHERE b.payment_status = 'Pending'
GROUP BY p.patient_id, p.first_name, p.last_name, b.payment_status
HAVING COUNT(a.appointment_id) > 1;
```

**Rank doctors by number of appointments using window functions:**
```sql
SELECT
    CONCAT(d.first_name, ' ', d.last_name) AS doctor_name,
    COUNT(a.appointment_id) AS total_appointments,
    RANK() OVER (ORDER BY COUNT(a.appointment_id) DESC) AS appointment_rank
FROM doctors d
LEFT JOIN appointments a ON d.doctor_id = a.doctor_id
GROUP BY d.doctor_id, d.first_name, d.last_name;
```

---

## 🎯 Interview Questions Included

The project ends with **10 real SQL interview questions** with full answers:

1. Doctor who treated the most unique patients
2. Patients with pending bills and multiple visits
3. Department with highest room charges
4. Currently admitted patients
5. Medications never prescribed
6. Patient bill classification using `CASE`
7. Doctors joined in last 5 years with high salary
8. Month-wise appointment trend
9. Duplicate phone number detection (data quality)
10. Self JOIN — doctor pairs in same department

---

## 🛠️ Requirements

- MySQL 8.0+ **or** PostgreSQL 13+
- Any SQL client: MySQL Workbench, DBeaver, pgAdmin, VS Code SQLTools

---

## 👤 Author

**Nitin**  
[LinkedIn](www.linkedin.com/in/nitin-kabde-a2a018313) • [GitHub](https://github.com/Nitin13-pix)

---

## ⭐ If this helped you, give it a star on GitHub!
