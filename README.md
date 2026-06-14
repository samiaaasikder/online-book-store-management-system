# 📚 Online Book Store Management System

> A full-stack web application for browsing, ordering, and managing books — built with PostgreSQL, Node.js/Express, React, and MongoDB.

**Developer:** Samia Sikder &nbsp;|&nbsp; **Roll:** 251035014 &nbsp;|&nbsp; **Duration:** 12 Weeks (June – August 2026)

---

## 🗂️ Table of Contents

- [Project Overview](#-project-overview)
- [Core Features](#-core-features)
- [Tech Stack](#-tech-stack)
- [System Architecture](#-system-architecture)
- [Database Schema](#-database-schema)
- [REST API Endpoints](#-rest-api-endpoints)
- [Project Roadmap](#-project-roadmap)
- [Folder Structure](#-folder-structure)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [Grading Breakdown](#-grading-breakdown)

---

## 📌 Project Overview

The **Online Book Store Management System** is a full-stack web application developed as part of the Database, Database Lab, and Software Engineering curriculum. It allows customers to browse a catalogue of books, manage their cart, place orders, and leave reviews — while giving admins full control over inventory, order fulfilment, and analytics.

| Field | Details |
|---|---|
| Project Type | Full Stack Web Application |
| Duration | 12 Weeks |
| Department | Computer Science & Engineering |
| Stack | PostgreSQL · Node.js · Express · React · MongoDB · Git |

---

## ✨ Core Features

- **User Authentication** — JWT-based login/signup, bcrypt password hashing, role-based access (Customer / Admin)
- **Book Catalogue** — Browse, search, and filter books by category, author, and price
- **Shopping Cart** — Add/remove items, quantity control, cart persistence
- **Order System** — Place orders, payment simulation, order history with status tracking
- **Admin Panel** — CRUD for books, authors, and categories; inventory and order management
- **Book Reviews** — Star ratings and text reviews stored in MongoDB
- **Analytics Dashboard** — Monthly sales, top customers, and revenue trends

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React, HTML5, CSS3, JavaScript |
| Backend | Node.js, Express.js |
| Relational DB | PostgreSQL, pgAdmin |
| NoSQL DB | MongoDB (reviews & activity logs) |
| Auth | JWT, bcrypt / Passlib |
| API Testing | Postman |
| Version Control | Git, GitHub |
| ORM | Sequelize / raw SQL |

---

## 🏗️ System Architecture

```
Customer / User
      │
      ▼
React Frontend  (HTML/CSS/JS)
      │  HTTP Requests
      ▼
Express Backend  (Node.js REST API)
      │
      ├──► PostgreSQL  (users, books, orders, cart)
      │
      └──► MongoDB     (reviews, activity logs)
```

---

## 🗄️ Database Schema

### PostgreSQL Tables

```sql
-- Users
CREATE TABLE Users (
    User_ID     SERIAL PRIMARY KEY,
    Name        VARCHAR(100) NOT NULL,
    Email       VARCHAR(150) UNIQUE NOT NULL,
    Password    VARCHAR(255) NOT NULL,  -- bcrypt hashed
    Role        VARCHAR(20)  DEFAULT 'customer',
    Created_At  TIMESTAMP    DEFAULT NOW()
);

-- Books
CREATE TABLE Books (
    Book_ID     SERIAL PRIMARY KEY,
    Title       VARCHAR(200) NOT NULL,
    Author_ID   INT REFERENCES Authors(Author_ID),
    Category_ID INT REFERENCES Categories(Category_ID),
    Price       DECIMAL(10,2) NOT NULL,
    Stock       INT DEFAULT 0,
    ISBN        VARCHAR(20) UNIQUE,
    Cover_URL   TEXT
);

-- Authors
CREATE TABLE Authors (
    Author_ID SERIAL PRIMARY KEY,
    Name      VARCHAR(100) NOT NULL,
    Bio       TEXT
);

-- Categories
CREATE TABLE Categories (
    Category_ID SERIAL PRIMARY KEY,
    Name        VARCHAR(100) NOT NULL,
    Description TEXT
);

-- Orders
CREATE TABLE Orders (
    Order_ID     SERIAL PRIMARY KEY,
    User_ID      INT REFERENCES Users(User_ID),
    Total_Amount DECIMAL(10,2),
    Status       VARCHAR(30) DEFAULT 'pending',
    Created_At   TIMESTAMP DEFAULT NOW()
);

-- Order_Items
CREATE TABLE Order_Items (
    Item_ID           SERIAL PRIMARY KEY,
    Order_ID          INT REFERENCES Orders(Order_ID),
    Book_ID           INT REFERENCES Books(Book_ID),
    Quantity          INT NOT NULL,
    Price_At_Purchase DECIMAL(10,2) NOT NULL
);
```

### MongoDB Collection (Reviews)

```json
{
  "book_id": "123",
  "user_id": "456",
  "rating": 4.5,
  "review_text": "Great book, highly recommended!",
  "likes": 12,
  "created_at": "2026-06-14T10:00:00Z"
}
```

---

## 🔌 REST API Endpoints

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| POST | `/register` | Register a new customer account | Public |
| POST | `/login` | Authenticate and receive JWT token | Public |
| GET | `/books` | List all books with filters & pagination | Public |
| GET | `/books/:id` | Get single book details | Public |
| POST | `/books` | Add a new book | Admin |
| PUT | `/books/:id` | Update book details | Admin |
| DELETE | `/books/:id` | Remove a book | Admin |
| GET | `/cart` | Retrieve current user's cart | Customer |
| POST | `/cart` | Add item to cart | Customer |
| POST | `/orders` | Place an order from cart | Customer |
| GET | `/orders/:id` | Get order details and status | Customer |
| GET | `/reviews/:bookId` | Get reviews for a book | Public |
| POST | `/reviews` | Submit a new review | Customer |
| GET | `/admin/stats` | Platform analytics and statistics | Admin |

---

## 🗺️ Project Roadmap

### 🚀 Phase 1 — Foundation & Design (Weeks 1–3)

| Week | Focus | Deliverables |
|---|---|---|
| Week 1 | Requirements & Planning | SRS Document, User Stories, Use Cases, DFD |
| Week 2 | ER Modeling | ER Diagram (7 entities), Relationships, PK/FK |
| Week 3 | Normalization & Schema | 3NF Schema, PostgreSQL Setup, DDL Scripts |

**⚑ Checkpoint 1:** SRS · ER Diagram · Normalized Schema · DDL Scripts · GitHub Repo

---

### 🚀 Phase 2 — SQL & Backend Core (Weeks 4–6)

| Week | Focus | Deliverables |
|---|---|---|
| Week 4 | Advanced SQL | JOIN Queries, Subqueries, Aggregations, Sample Data |
| Week 5 | Transactions & Triggers | BEGIN/COMMIT/ROLLBACK, Stock Triggers, Payment Flow |
| Week 6 | REST API & SE Design | Express Backend, MVC Structure, Swagger Docs, Postman |

**✦ Checkpoint 2 (Midterm):** Live SQL demo · 3+ APIs · Transaction rollback · DB Viva

---

### 🚀 Phase 3 — Optimization & Advanced DB (Weeks 7–9)

| Week | Focus | Deliverables |
|---|---|---|
| Week 7 | Indexing & Performance | Indexes, EXPLAIN ANALYZE, Before/After Report |
| Week 8 | Stored Procedures & Views | Place Order Procedure, Invoice Generator, Revenue View |
| Week 9 | NoSQL & Data Import | MongoDB Reviews, Activity Logs, CSV Import |

**⚑ Checkpoint 3:** Performance Report · Stored Procedures · MongoDB Integration · CSV Script

---

### 🚀 Phase 4 — Frontend, Testing & SE (Weeks 10–11)

| Week | Focus | Deliverables |
|---|---|---|
| Week 10 | Frontend & SDLC | React UI (Homepage, Cart, Checkout, Admin), Agile Sprints |
| Week 11 | Testing & Security | Unit + Integration Tests, SQL Injection Prevention, Roles |

**✦ Checkpoint 4:** Full working app · Test report · Security checklist · Git workflow proof

---

### 🚀 Phase 5 — Final Polish & Presentation (Week 12)

| Week | Focus | Deliverables |
|---|---|---|
| Week 12 | Final Demo & Documentation | Analytics Dashboard, Final Report, Live Demo, Viva Prep |

**★ Final Evaluation:** Live demo · Viva (DB + SE + Lab) · GitHub submission · Peer evaluation

---

## 📁 Folder Structure

```
online-book-store/
│
├── backend/
│   ├── controllers/        # Route handlers (books, orders, auth, cart)
│   ├── models/             # Sequelize models / raw SQL queries
│   ├── routes/             # Express route definitions
│   ├── middleware/         # JWT auth, role guard, error handler
│   ├── config/             # DB connection (PostgreSQL + MongoDB)
│   ├── utils/              # Helper functions
│   └── server.js           # Entry point
│
├── frontend/
│   ├── public/
│   └── src/
│       ├── components/     # Reusable React components
│       ├── pages/          # Homepage, BookDetail, Cart, Checkout, Admin
│       ├── context/        # Auth context, Cart context
│       ├── services/       # Axios API calls
│       └── App.jsx
│
├── database/
│   ├── schema.sql          # DDL scripts (CREATE TABLE)
│   ├── seed.sql            # Sample data
│   ├── triggers.sql        # Stock triggers
│   ├── procedures.sql      # Stored procedures
│   └── views.sql           # Best-sellers, revenue views
│
├── ml/                     # (optional) Analytics scripts
├── docs/
│   ├── SRS.pdf
│   ├── ER_Diagram.png
│   └── API_Docs.md
│
├── .env.example
├── .gitignore
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- Node.js v18+
- PostgreSQL 15+
- MongoDB 6+
- Git

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/your-username/online-book-store.git
cd online-book-store

# 2. Install backend dependencies
cd backend
npm install

# 3. Install frontend dependencies
cd ../frontend
npm install

# 4. Setup PostgreSQL database
psql -U postgres -f database/schema.sql
psql -U postgres -f database/seed.sql

# 5. Run the backend server
cd ../backend
npm run dev

# 6. Run the React frontend
cd ../frontend
npm start
```

The app will be available at `http://localhost:3000` and the API at `http://localhost:5000`.

---

## 🔐 Environment Variables

Create a `.env` file in the `backend/` folder:

```env
# Server
PORT=5000

# PostgreSQL
DB_HOST=localhost
DB_PORT=5432
DB_NAME=bookstore
DB_USER=postgres
DB_PASSWORD=your_password

# MongoDB
MONGO_URI=mongodb://localhost:27017/bookstore_reviews

# JWT
JWT_SECRET=your_jwt_secret_key
JWT_EXPIRES_IN=7d

# bcrypt
BCRYPT_ROUNDS=10
```

---

## 📊 Grading Breakdown

| Milestone | Weight | Covers |
|---|---|---|
| Checkpoint 1 — SRS + Schema | 20% | Requirements, ER Diagram, Normalized SQL |
| Checkpoint 2 — Midterm | 25% | SQL Queries, REST APIs, Transactions Demo |
| Checkpoint 3 — Optimization | 15% | Indexing, Stored Procedures, MongoDB |
| Checkpoint 4 — Testing + UI | 15% | React Frontend, Test Report, Security |
| Final Demo + Viva | 25% | Live Application, Presentation, Peer Evaluation |

---

## 🎯 Target Outcomes

- Full Stack project with React frontend + Express backend
- REST API development — all endpoints Postman-tested and documented
- Secure authentication — JWT, bcrypt, role-based access control
- Normalized PostgreSQL schema with ER diagram and DDL scripts
- NoSQL integration — MongoDB for reviews and activity logs
- Advanced SQL — transactions, triggers, stored procedures, views, indexing
- Software Engineering practices — Agile, Git branching, MVC, testing

---

<div align="center">

**Online Book Store Management System**

Samia Sikder &nbsp;·&nbsp; Roll: 251035014 &nbsp;·&nbsp; Version 1.0 &nbsp;·&nbsp; June 2026

</div>
