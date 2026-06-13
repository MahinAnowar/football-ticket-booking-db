# Football Ticket Booking System — Database (PostgreSQL)

A relational database for a football ticket booking platform that manages fans, tournament matches, and the ticket bookings that connect them.

> **Submitted by:** Mahin Anowar &nbsp;|&nbsp; **Database:** PostgreSQL

## 🔗 Submission Links

| Item | Link |
| --- | --- |
| **ERD Diagram (Public)** | _add draw.io link here_ |
| **GitHub Repository** | https://github.com/MahinAnowar/football-ticket-booking-db |
| **Interview Video** | _add video link here_ |

## 📦 What I Built

- **[QUERY.sql](./QUERY.sql)** — the complete solution:
  - **Schema (DDL)** for 3 tables with primary keys, foreign keys, and `CHECK` constraints
  - **Sample data** seeding for all tables
  - **7 analytical SQL queries** (Part 2 of the task)
- **[ERD.drawio](./ERD.drawio)** — the Entity Relationship Diagram (open in [draw.io](https://app.diagrams.net))

## 🧱 Database Design

| Table | Purpose |
| --- | --- |
| **Users** | Platform users — `Football Fan` and `Ticket Manager` roles |
| **Matches** | Football fixtures with pricing and availability status |
| **Bookings** | Individual ticket purchases linking a user to a match |

**Relationships**
- One **User** → many **Bookings** (`Bookings.user_id` → `Users.user_id`)
- One **Match** → many **Bookings** (`Bookings.match_id` → `Matches.match_id`)

## 🧠 SQL Concepts Covered

Filtering with `WHERE`, `ILIKE` pattern matching, `COALESCE` / `NULL` handling, `INNER JOIN`, `LEFT JOIN`, scalar subqueries with `AVG`, and `LIMIT` / `OFFSET` pagination.

## ▶️ How to Run

Run the full script against any PostgreSQL database (e.g. [Neon](https://neon.tech) or local `psql`):

```bash
psql "<your-connection-string>" -f QUERY.sql
```

It drops and recreates the tables, seeds the sample data, and includes all 7 queries ready to execute.
