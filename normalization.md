# 🧮 Database Normalization: Airbnb Schema

This document explains the normalization process applied to the Airbnb database schema to ensure it meets **Third Normal Form (3NF)**.

---

## ✅ Normalization Rules Recap

- **1NF**: All fields must contain atomic values, and there should be no repeating groups.
- **2NF**: All non-key attributes must depend on the whole primary key.
- **3NF**: No transitive dependencies — every non-key attribute must depend only on the primary key.

---

## 🔍 Analysis of Original Schema

| Table     | Issue Identified                              | Resolution                              |
|-----------|------------------------------------------------|------------------------------------------|
| `Booking` | `status` as ENUM                               | Moved to a new `BookingStatus` table     |
| `Booking` | `total_price` derived from other fields        | Removed to avoid redundancy              |
| `Payment` | `amount` may duplicate `Booking.total_price`   | Kept only if partial payments are allowed|

---

## ✅ Applied Fixes to Achieve 3NF

### 1. Created `BookingStatus` Table

```sql
CREATE TABLE BookingStatus (
  status_id INT PRIMARY KEY,
  status_name VARCHAR(50) UNIQUE NOT NULL
);
