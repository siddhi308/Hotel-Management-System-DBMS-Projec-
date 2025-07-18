
# 🏨 Hotel Management System (DBMS Project)

This project is a **Hotel Management System** built using database principles, with complete front-end, back-end, and database integration. It demonstrates table design, ER modeling, SQL queries, and web technology for full-stack execution.

---

## 👩‍💻 Team Members
- **Mayuri Gadhave**
- **Tanya Gadwal**
- **Anushka Gaikwad**
- **Siddhi Shinde**

---

## 🧰 Technology Stack

### 🔹 Front-End
- **HTML**, **CSS**, **JavaScript**
- **ISP** (Java + HTML on one page)

### 🔹 Back-End
- **Java Servlets**
- **Tomcat Server**
- **Eclipse IDE (Enterprise Edition)**

### 🔹 Database
- **MySQL**
- Connected via **JDBC**

---

## 🗃️ Database Tables

### 1. `Employee`
```sql
create table Employee (
    empID int primary key AUTO_INCREMENT,
    empName varchar(100) not null,
    empAge int not null,
    empGender varchar(20),
    empDepartment varchar(50),
    empSalary int not null,
    empPhNo varchar(12) unique,
    empAaddhar varchar(15) unique,
    empEmail varchar(20)
);
```

### 2. `Customer`
```sql
create table Customer (
    custID int primary key AUTO_INCREMENT,
    custName varchar(50) not null,
    custAge int not null,
    custPhNo varchar(12) unique,
    custAadharNo varchar(15) unique,
    custCountry varchar(50)
);
```

### 3. `Room`
```sql
create table Room (
    roomID int primary key,
    roomPrice int not null,
    roomBedType varchar(30)
);
```

### 4. `custRoom` (Customer-Room Relationship)
```sql
create table custRoom (
    custID int,
    roomID int,
    checkInDt date,
    checkOutDt date,
    deposit int,
    bookingDt date,
    primary key(custID, roomID, checkInDt),
    foreign key(custID) references Customer(custID),
    foreign key(roomID) references Room(roomID)
);
```

### 5. `Amenities`
```sql
create table Amenities (
    amenityID int primary key,
    amenityName varchar(50) unique,
    amenityPrice int not null
);
```

### 6. `CustAmenity`
```sql
create table CustAmenity (
    custAmenityID int primary key AUTO_INCREMENT,
    custID int not null,
    amenityID int not null,
    usedDate date,
    foreign key(custID) references Customer(custID),
    foreign key(amenityID) references Amenities(amenityID)
);
```

---

## 🧾 Sample Queries

### 📌 Employee
- Insert: `INSERT INTO Employee (...) VALUES (...);`
- View all: `SELECT * FROM Employee;`
- Filter by department: `SELECT * FROM Employee WHERE empDepartment = ?;`
- Top salaries: `SELECT * FROM Employee ORDER BY empSalary DESC LIMIT 3;`

### 📌 Customer
- Insert: `INSERT INTO Customer (...) VALUES (...);`
- Available rooms: `SELECT roomID FROM Room WHERE roomID NOT IN (SELECT roomID FROM custRoom);`
- View: `SELECT * FROM Customer;`
- Delete: `DELETE FROM Customer WHERE custID = ?;`

### 📌 Room & Amenities
- Get room types: `SELECT roomBedType, COUNT(*) FROM Room GROUP BY roomBedType;`
- View amenities: `SELECT * FROM Amenities;`
- Join: `SELECT * FROM CustAmenity LEFT OUTER JOIN Amenities ON CustAmenity.amenityID = Amenities.amenityID;`

### 📌 Views & Functions
- Create view:
```sql
CREATE VIEW Cust3 AS
SELECT Customer.custID, custName, roomID
FROM Customer, custRoom
WHERE Customer.custID = custRoom.custID;
```

- Date functions:
```sql
SELECT DATEDIFF(checkOutDt, checkInDt) AS daysStayed FROM custRoom;
SELECT DATE_FORMAT(checkInDt, '%D %b %Y') FROM custRoom;
```

---

## 🧩 ER Diagram & Normalization

- All tables are normalized up to **3NF**.
- Redundancy is minimized.
- Composite keys used in relationship tables.

---

## 🧠 Key Features
- Full CRUD operations for **Employee**, **Customer**, and **Rooms**
- Relational integrity using **foreign keys**
- Dynamic views and analysis queries
- **Frontend-Backend integration** using Servlets
- Interactive and normalized database design

---

## 🙏 Thank You!

This project is a real-time example of how databases and web technologies integrate for a hotel management system. Contributions by our team ensure modularity, clarity, and functionality across components.
