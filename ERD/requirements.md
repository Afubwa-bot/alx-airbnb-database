# 🏠 Airbnb Database Schema Overview 

This project documents the relational database schema for an Airbnb-like platform. It outlines how core entities like users, properties, bookings, payments, reviews, and messages interact within the system.

---

## Entity Breakdown & Flow 

### 🔹 1. `User` Table

Stores information about **all users** on the platform.

- `user_id`: Primary Key (used by all other tables to reference the user)
- `role`: `guest`, `host`, or `admin`

#### ⏬ Used by:

- `Property.host_id` → shows which host owns a property  
- `Booking.user_id` → which guest made the booking  
- `Review.user_id` → who left a review  
- `Message.sender_id` and `recipient_id` → messaging between users  

---

### 🔹 2. `Property` Table

Stores information about **properties** listed by hosts.

- `host_id`: Foreign Key → connects to `User.user_id`  
- A host can have **many properties** (1:N)

#### ⏬ Used by:

- `Booking.property_id` → guests book these properties  
- `Review.property_id` → users review these properties  

---

### 🔹 3. `Booking` Table

Stores every **reservation** made by a guest.

- `user_id`: Foreign Key → the guest who made the booking  
- `property_id`: Foreign Key → the property being booked  
- `status`: `pending`, `confirmed`, or `canceled`

#### ⏬ Used by:

- `Payment.booking_id` → one payment per booking  

---

### 🔹 4. `Payment` Table

Stores **payment details** for bookings.

- `booking_id`: Foreign Key → ties the payment to the correct booking  
- `payment_method`: `credit_card`, `paypal`, `stripe`

#### 🔁 Logic:

Every **booking has one payment**, and you can trace payments back to the user via `Booking`.

---

### 🔹 5. `Review` Table

Stores **user reviews** about properties.

- `user_id`: Foreign Key → the user writing the review  
- `property_id`: Foreign Key → the property being reviewed  
- `rating`: Integer between 1–5 (CHECK constraint)

#### 🔁 Logic:

A user can review a property **only after staying there** (enforced by app logic).

---

### 🔹 6. `Message` Table

Stores **conversations** between users.

- `sender_id` and `recipient_id`: Both reference `User.user_id`  
- `message_body`: stores the actual text  
- Used for **guest-host communication** before booking

---

## 🔄 Complete Flow (Step-by-Step)

Here’s how a typical Airbnb use-case plays out through your schema:

1. A **user signs up** → info goes into the `User` table.  
2. If they’re a **host**, they list a new **property** → stored in the `Property` table with `host_id = user_id`.  
3. A **guest browses** properties and books one → info goes to the `Booking` table.  
4. The system creates a **payment** → entry in `Payment` table linked to the booking.  
5. After the stay, the guest writes a **review** → entry in `Review` table.  
6. Throughout the process, guest and host may **message** each other → entries in the `Message` table.  

---

## 🧠 Relationships Summary

| Table    | References                      | Related To                        |
|----------|----------------------------------|-----------------------------------|
| Property | User (`host_id`)                | A host owns a property            |
| Booking  | User (`user_id`), Property      | A guest books a property          |
| Payment  | Booking (`booking_id`)          | Payment is for a booking          |
| Review   | User (`user_id`), Property      | User reviews a property           |
| Message  | User (`sender_id`, `recipient_id`) | User-to-user communication    |

---

> 📌 This schema is designed for scalability, data consistency, and clean separation of concerns — the foundation for a robust vacation rental platform.
> 
