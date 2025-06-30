# 🧪 Database Seeding Script (`seed.sql`)

This directory contains the **SQL Data Manipulation Language (DML)** script for populating the `alx_airbnb` database with **realistic sample data**.

## 📌 Purpose

The `seed.sql` file complements the `schema.sql` by inserting a complete set of sample data that mimics real-world Airbnb usage. This is essential for:
- Local development and UI testing
- Backend logic testing (e.g., filtering, searching, booking logic)
- Demo or presentation scenarios

---

## 📄 Tables Populated

Data is inserted in a **logical order** to satisfy foreign key constraints and application behavior:

1. **User** – Creates a variety of users with roles like `host`, `guest`, and `admin`.
2. **Property** – Adds property listings tied to hosts.
3. **Booking** – Simulates bookings across different time ranges (past, current, future).
4. **Payment** – Records corresponding payments (full and partial).
5. **Review** – Inserts feedback left by guests after completed stays.
6. **Message** – Simulates in-app communication between users.

---

## 🚀 How to Use

### ✅ Prerequisites

Before running this script, make sure you:
- Have a working MySQL/MariaDB setup
- Already executed the `schema.sql` script successfully to create the database structure

### 🧭 Steps

#### 1. **Select the Target Database**
Make sure you're using the correct database:
```sql
USE alx_airbnb;
