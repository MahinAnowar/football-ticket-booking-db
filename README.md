# Football Ticket Booking System — Database (PostgreSQL)

A relational database for a football ticket booking platform that manages fans, tournament matches, and the ticket bookings that connect them.

> **Submitted by:** Mahin Anowar &nbsp;|&nbsp; **Database:** PostgreSQL

## 🔗 Submission Links

| Item | Link |
| --- | --- |
| **ERD Diagram (Public)** | [View ERD on draw.io](https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=ERD.drawio&dark=auto#R%3Cmxfile%3E%3Cdiagram%20name%3D%22Football%20Ticket%20Booking%20ERD%22%20id%3D%22football-erd%22%3E7Vptc5s4EP41nmk%2FXAZE4OhHG%2BM20zrtJZe79pNHBsXWRCCPEIndX38rIQIEcr1rRZNx6mFsdrV62X0WeFZm4kXZ%2Fq3Au%2B2Sp4RNkJPuJ958gpDruD78KM2h0gRBUCk2gqbGqFFc0q%2Bk7mm0JU1J0TGUnDNJd11lwvOcJLKjw0Lwu67ZNWfdWXd4Q3qKywSzvvZvmsqt0bqO0zS8I3SzNVOHvmnIcG1sFMUWp%2FyupfLiiRcJzmV1lu0jwlTw6rhU%2FRaPtN4vTJBc%2FpcOZUFE0e9kxinkoXa5uKMZwzlIs2uey0vT4tZyhZF7CjJmdJODkMBwRIDilghJIXpT0yD5DrTJlrL0Az7wUk1aSJzc1NJsywX9CsNiZuaAZlFPgsKOxaXqCWoHtIIUYPOp9sR9oFrivTFMOGN4V9C19kJpMiw2NJ9xKXlmVLXPC8pYxBkXOhTeQn%2BU4139fBqHi0gvVvAb0moJojCeqR5VWG8xK01Yr5r4qyiRfSv%2BBrG3hGdEigOYbFs55fph1e%2BuyUAUmLQyw5wa8dAVsUn%2Fzf3ITYbAiUmSRxJmIMVaSdTKGHBG9oKR8yqFWpEzqjprGLmWAzmT0TRVI8%2BKHU5ovvmgzeau8yAhVQLuOM2l9tGfwQFeR86JP%2FFhVRHIbiPDocyFjHgOC8VUu0RwIe9IIYcAU76uIBhwXXlT%2BD47%2F1OdV4c%2F%2B%2FReT%2FMdeKLgcTgNfii0gB96fviNidd1ydgqxxm5R%2Byv6UX0bnrxCu7Wr8dCyj%2B1gJT3spAiGaashxLy%2FdftC%2Bzq%2FOyPq3jEiyy0cZM8fVnQCc761xdyOsAtcK7PF%2FC9xDkwJDEiiq4TWIDRf1kw7rawvFVeZmvAZhDOkcDy0I%2BDBdQ62ZJfXNYSl%2FXjUHOpHpcN0cyDcm0gfZZtBCywWc%2FpstkgsE9nswE628mkoye02tufxWjvIbXIaLMBRvv0EI7KaelelmKA0fr27tEPkbLBaLMBRnvcSEleClV85HKVYEk2XId%2BvDrkIWo2yGw2QGaPG7U1LsgKVnJD5GonaNJcaedXy%2FjiLHqlNiIjNBpsVthrNsBejxu36lEG9EqWxbfKkektVJt4XdUtuii5VLvAyPkIpA05JycnIz72rBDeNec3ENxfjNcO410s4iAa3L2d%2F%2F5m5jhDCTfrQPB%2FKW942q%2BMwi7l9XqU18INfT3AebvJdPSk17j70zZyQ%2Fu0dz1Ae58Ziuhp9%2BIX7%2BH3twkKNlVvp%2FqzZTxYbXDk9QBHfmGwfqsi7eFabzyMh6wNHr0e4NHPANkxkSwIlo%2FtJ7oW9xPDEejzeoA%2BHzlcO3zQpeq%2FMeiRELNCiIMXh5jkQKFXCS%2Fk2CVqDzHfAochhomStPe%2BTb%2Ba4aVIavqGeniqIeoHFHSl8nBBGJaU53HT0il2VHmxlVldowhe5ilJTfFA8nSqXhQCMb7IcJ5%2B1GmgC5lOw0EZ76n8XHeE8y%2FqHCCtpPm%2B1TQ%2F3E8AsfrcGCrxi1mKFppuWqr7VY7DMjak%2FkfK7aWFWmxFd8xDM0aTMJi8QZW4VMtGTrt66eeD0OG77eLyQ2Cj7wTbe5Zgu08CdvYY2JoDPR3aIDYvrem21qt%2FXvwP%3C%2Fdiagram%3E%3C%2Fmxfile%3E) |
| **GitHub Repository** | https://github.com/MahinAnowar/football-ticket-booking-db |

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
