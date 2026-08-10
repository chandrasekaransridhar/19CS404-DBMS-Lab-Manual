# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:

<img width="10300" height="5108" alt="image" src="https://github.com/user-attachments/assets/bcb3e730-1718-453f-9dfc-f4f07925285e" />

### Entities and Attributes

| Entity          | Attributes (PK, FK)                                                          | Notes                          |
| --------------- | ---------------------------------------------------------------------------- | ------------------------------ |
| Member          | Member_ID (PK), Name, Membership_Type, Start_Date                            | Stores member details          |
| Program         | Program_ID (PK), Program_Name                                                | Yoga, Zumba, Weight Training   |
| Trainer         | Trainer_ID (PK), Trainer_Name                                                | Stores trainer details         |
| Member_Program  | Member_ID (PK, FK), Program_ID (PK, FK)                                      | Connects members and programs  |
| Program_Trainer | Program_ID (PK, FK), Trainer_ID (PK, FK)                                     | Connects programs and trainers |
| Session         | Session_ID (PK), Member_ID (FK), Trainer_ID (FK), Session_Date, Session_Time | Personal training booking      |
| Attendance      | Attendance_ID (PK), Session_ID (FK), Status                                  | Records attendance             |
| Payment         | Payment_ID (PK), Member_ID (FK), Payment_Type, Amount, Payment_Date          | Records payments               |

### Relationships and Constraints

| Relationship                | Cardinality | Participation | Notes                                   |
| --------------------------- | ----------- | ------------- | --------------------------------------- |
| Member joins Program        | M:N         | Partial       | Member can join multiple programs       |
| Program assigned to Trainer | M:N         | Partial       | Program can have multiple trainers      |
| Member books Session        | 1:M         | Partial       | Member can book many sessions           |
| Trainer conducts Session    | 1:M         | Partial       | Trainer can conduct many sessions       |
| Session has Attendance      | 1:1         | Total         | Attendance is recorded for each session |
| Member makes Payment        | 1:M         | Partial       | Member can make multiple payments       |

### Assumptions

1. Each member has a unique Member_ID.
2. Each trainer has a unique Trainer_ID.
3. Each program has a unique Program_ID.
4. A member can join multiple programs.
5. A program can have multiple trainers.
6. A member can book multiple training sessions.
7. Each session belongs to one member and one trainer.
8. Attendance is recorded for each session.
9. A member can make multiple payments.
10. Payment amount must be greater than zero.

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="7168" height="4008" alt="image" src="https://github.com/user-attachments/assets/ed19ec44-2375-41e7-be3b-b2535622e61d" />

### Entities and Attributes

| Entity       | Attributes (PK, FK)                                                | Notes              |
| ------------ | ------------------------------------------------------------------ | ------------------ |
| Member       | Member_ID (PK), Member_Name, Phone, Email                          | Library member     |
| Book         | Book_ID (PK), Title, Author, Category                              | Book details       |
| Loan         | Loan_ID (PK), Member_ID (FK), Book_ID (FK), Loan_Date, Return_Date | Book lending       |
| Event        | Event_ID (PK), Event_Name, Event_Date, Event_Time                  | Library events     |
| Speaker      | Speaker_ID (PK), Speaker_Name, Author_Name                         | Event speakers     |
| Room         | Room_ID (PK), Room_Name, Capacity                                  | Library rooms      |
| Registration | Registration_ID (PK), Member_ID (FK), Event_ID (FK)                | Event registration |
| Fine         | Fine_ID (PK), Loan_ID (FK), Amount, Fine_Date, Paid_Status         | Overdue fine       |


### Relationships and Constraints

| Relationship           | Cardinality | Participation | Notes                            |
| ---------------------- | ----------- | ------------- | -------------------------------- |
| Member borrows Book    | M:N         | Partial       | Through Loan                     |
| Member registers Event | M:N         | Partial       | Through Registration             |
| Event has Speaker      | M:N         | Total         | Event can have multiple speakers |
| Event uses Room        | 1:M         | Total         | Room booked for events           |
| Loan generates Fine    | 1:1         | Partial       | Fine only for overdue books      |


### Assumptions
1. A member can borrow multiple books.
2. A book can be borrowed by different members at different times.
3. A member can register for multiple events.
4. Each event has at least one speaker.
5. A fine is generated only when a book is returned late.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="5848" height="4724" alt="image" src="https://github.com/user-attachments/assets/d6002ca7-a8c4-4906-8ce5-ce0d49f81f3d" />


### Entities and Attributes

| Entity      | Attributes (PK, FK)                                                                                                          | Notes                       |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------- | --------------------------- |
| Customer    | Customer_ID (PK), Customer_Name, Phone                                                                                       | Customer details            |
| Table       | Table_ID (PK), Table_Number, Capacity                                                                                        | Restaurant table            |
| Reservation | Reservation_ID (PK), Customer_ID (FK), Table_ID (FK), Reservation_Date, Reservation_Time, Number_of_Guests, Reservation_Type | Reservation/walk-in details |
| Order       | Order_ID (PK), Reservation_ID (FK), Order_Date                                                                               | Food order                  |
| Dish        | Dish_ID (PK), Dish_Name, Price, Category_ID (FK)                                                                             | Food items                  |
| Category    | Category_ID (PK), Category_Name                                                                                              | Starter, Main, Dessert      |
| Order_Item  | Order_ID (PK, FK), Dish_ID (PK, FK), Quantity                                                                                | Items in each order         |
| Bill        | Bill_ID (PK), Reservation_ID (FK), Food_Amount, Service_Charge, Total_Amount                                                 | Billing details             |
| Waiter      | Waiter_ID (PK), Waiter_Name                                                                                                  | Waiter details              |


### Relationships and Constraints

| Relationship                 | Cardinality | Participation | Notes                                |
| ---------------------------- | ----------- | ------------- | ------------------------------------ |
| Customer makes Reservation   | 1:M         | Partial       | Customer can make many reservations  |
| Reservation books Table      | M:1         | Total         | One reservation uses one table       |
| Reservation has Order        | 1:M         | Partial       | Reservation can have multiple orders |
| Order contains Dish          | M:N         | Total         | Through Order_Item                   |
| Category contains Dish       | 1:M         | Total         | Category has many dishes             |
| Reservation generates Bill   | 1:1         | Total         | One bill per reservation             |
| Reservation served by Waiter | M:N         | Partial       | Through Reservation_Waiter           |


### Assumptions
1. A customer can make multiple reservations.
2. Each reservation is assigned to one table.
3. A reservation can contain multiple food orders.
4. Each order can contain multiple dishes.
5. Dishes belong to one category.
6. One bill is generated for each reservation.
7. A reservation can be served by one or more waiters.
---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
