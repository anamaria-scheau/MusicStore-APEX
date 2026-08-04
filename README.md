# 🎵 MusicStore APEX

### A Complete Web Application for Music Store Management

---

##  Project Overview

**MusicStore APEX** is a fully functional web application developed using **Oracle APEX** for managing a physical or online music store specializing in vinyl records, CDs, and audio cassettes. The application provides comprehensive support for managing products, artists, albums, genres, customers, orders, and inventory.

This project was developed as part of the **Cloud Data Engineering** course within the **Multimedia Technologies** Master's program at the Technical University of Cluj-Napoca.

---

##  IMPORTANT NOTICE

**My Oracle APEX account has been purged/deactivated.**  
The live application is no longer accessible online.

### What's Included in This Repository:
-  **Complete project documentation** 
-  **SQL DDL scripts** 
-  **Database design documentation**

This documentation serves as the **primary evidence** of the completed project work.

---

##  Project Objectives

The application supports the following business activities:

| Feature | Description |
|---------|-------------|
|  **Product Management** | Add and manage vinyl records, CDs, and cassettes |
|  **Artist Management** | Maintain artist information and discography |
|  **Album Management** | Organize albums with genres and release years |
|  **Inventory Control** | Track stock levels for all products |
|  **Customer Management** | Manage customer profiles and contact details |
|  **Order Processing** | Create and view customer orders |
|  **Sales Reporting** | Generate reports on sales and product performance |

---

##  Database Design

### Entity-Relationship Model

The database was designed using **SQL Developer Data Modeler** and normalized to **Third Normal Form (3NF)** to ensure data integrity and eliminate redundancy.

### Core Tables

```
 DATABASE SCHEMA
├── ARTIST          (id_artist, nume, tara)
├── GEN_MUZICAL     (id_gen, denumire)
├── ALBUM           (id_album, titlu, an_lansare, artist_id, gen_id)
├── PRODUS          (id_produs, tip_format, pret, stoc, album_id)
├── CLIENT          (client_id, nume, prenume, email, telefon)
├── COMANDA         (id_comanda, data_comanda, total, client_id)
└── DETALII_COMANDA (id_comanda, id_produs, cantitate, pret_unitar)
```

### Business Rules

| Relationship | Cardinality | Description |
|--------------|-------------|-------------|
| **ARTIST → ALBUM** | 1 : N | One artist can release multiple albums |
| **GEN → ALBUM** | 1 : N | One genre can include multiple albums |
| **ALBUM → PRODUS** | 1 : N | One album can have multiple formats (vinyl, CD, cassette) |
| **CLIENT → COMANDA** | 1 : N | One client can place multiple orders |
| **COMANDA → DETALII** | 1 : N | One order can contain multiple product lines |
| **PRODUS → DETALII** | 1 : N | One product can appear in multiple orders |

### Normalization

The database is fully normalized to **3NF**:

| Normal Form | Implementation |
|-------------|----------------|
| **1NF** | All values are atomic; each table has a primary key |
| **2NF** | All non-key attributes depend on the entire primary key |
| **3NF** | No transitive dependencies between non-key attributes |

---

##  Application Features

### 1. Dashboard

The main page provides a comprehensive overview of store activity:

####  Column Chart – Sales by Album
- Visualizes total sales for each album
- Helps identify best-selling albums
- Data sourced from `DETALII_COMANDA` with calculated totals

####  Order Calendar
- Displays all orders on a calendar interface
- Shows order date, total amount, and client name
- Tooltips provide additional order information

### 2. Forms

####  Client Form
- Fields: Name, Surname, Email, Phone
- **Required fields**: Name, Surname, Phone
- Visual validation for mandatory fields
- Confirmation message on successful submission

####  Order Form
- Fields: Order Date, Total Amount, Client (dropdown)
- Client dropdown shows full names
- Maintains referential integrity with `CLIENT` table
- Automatic data validation

### 3. Reports

####  Classic Report – Orders with Clients
- Displays all orders with client information
- Shows: Order ID, Client Name, Order Date, Total
- Uses JOIN between `COMANDA` and `CLIENT`

####  Interactive Report – Products, Albums & Artists
- Shows: Format, Price, Stock, Album Title, Artist Name
- **Interactive features**: Filtering, sorting, searching
- Uses JOIN between `PRODUS`, `ALBUM`, and `ARTIST`

---

##  Technologies Used

| Technology | Purpose |
|------------|---------|
| **Oracle APEX** | Web application development |
| **Oracle SQL** | Database management |
| **SQL Developer Data Modeler** | Database design and modeling |

---

##  Repository Structure

```
musicstore-apex/
│
├── README.md                                    # This file
├── MusicStore APEX.pdf                          #  Complete project documentation
├── ddl proiect.ddl                              #  Database DDL script
└── ..
```

---

##  Documentation

The complete project documentation includes:

-  **Database Design** (ERD and Relational Diagrams)
-  **Business Rules** (Cardinalities and relationships)
-  **Normalization Explanation** (1NF, 2NF, 3NF)
-  **Application Features** (Detailed descriptions)
-  **SQL DDL Script** (Complete CREATE statements)
-  **Application Screenshots** (All pages and components)

**[ View Full Documentation](MusicStore APEX.pdf)**

---

##  SQL Script

The DDL script includes:

| Component | Count |
|-----------|-------|
| Tables Created | 7 |
| Primary Keys | 7 |
| Foreign Keys | 6 |
| Sequences | 1 |
| Triggers | 1 |

### Key Objects:

```sql
-- Tables
ARTIST, GEN_MUZICAL, ALBUM, PRODUS, CLIENT, COMANDA, DETALII_COMANDA

-- Foreign Key Relationships
ALBUM → ARTIST, GEN_MUZICAL
PRODUS → ALBUM
COMANDA → CLIENT
DETALII_COMANDA → COMANDA, PRODUS

-- Auto-increment Sequence & Trigger
CLIENT_CLIENT_ID_SEQ
CLIENT_CLIENT_ID_TRG
```

**[ View DDL Script](ddl proiect.ddl)**

---

##  Project Context

| Detail | Information |
|--------|-------------|
| **University** | Technical University of Cluj-Napoca |
| **Faculty** | Electronics, Telecommunications and Information Technology |
| **Specialization** | Multimedia Technologies |
| **Course** | Cloud Data Engineering |
| **Coordinator** | Conf. Dr. Ing. Bogdan Orza |

---

##  Author

**Scheau Anamaria**  
Master's Student - Multimedia Technologies  
Technical University of Cluj-Napoca

---

##  Key Learning Outcomes

This project demonstrates:

-  Database design and normalization (1NF → 2NF → 3NF)
-  Creating Entity-Relationship Diagrams using SQL Developer Data Modeler
-  Implementing business rules in a relational database
-  Developing a complete web application using Oracle APEX
-  Creating interactive dashboards with charts and calendars
-  Building forms with client-side validation
-  Generating complex reports with JOIN queries
-  Maintaining data integrity with foreign keys and constraints

---

##  Sample Queries

### Top Albums by Sales
```sql
SELECT a.titlu AS album, 
       SUM(dc.cantitate * dc.pret_unitar) AS total_sales
FROM detalii_comanda dc
JOIN produs p ON dc.produs_id_produs = p.id_produs
JOIN album a ON p.album_id_album = a.id_album
GROUP BY a.titlu
ORDER BY total_sales DESC;
```

### Orders with Client Information
```sql
SELECT c.id_comanda, 
       cl.nume || ' ' || cl.prenume AS client,
       c.data_comanda, 
       c.total
FROM comanda c
JOIN client cl ON c.client_client_id = cl.client_id;
```

### Products with Album and Artist
```sql
SELECT p.tip_format, 
       p.pret, 
       p.stoc, 
       a.titlu AS album,
       ar.nume AS artist
FROM produs p
JOIN album a ON p.album_id_album = a.id_album
JOIN artist ar ON a.artist_id_artist = ar.id_artist;
```

---



**© 2025 Scheau Anamaria** - All Rights Reserved

---

*This project was developed for educational purposes as part of the Multimedia Technologies Master's program at the Technical University of Cluj-Napoca.*
