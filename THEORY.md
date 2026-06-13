# Part 3 — Theory Answers (Viva Practice)

> The assignment asks you to answer **any 3** in writing and speak about **any 2** on video.
> All five are answered below so you can pick the ones you're most comfortable explaining.
> Speak naturally in your own words — these notes are your understanding, not a script to read.

---

## Question 1 — What role does a Foreign Key play in the Bookings table, and how does it stop a ticket sale for a match that doesn't exist?

A **Foreign Key (FK)** is a column in one table that points to the **Primary Key** of another table. In the `Bookings` table, `user_id` is a foreign key to `Users(user_id)` and `match_id` is a foreign key to `Matches(match_id)`. This creates a parent–child link between the tables.

Its job is to enforce **referential integrity** — the rule that a booking can only reference a user and a match that *actually exist*. If someone tries to insert a booking with `match_id = 999` when no match `999` exists, the database **rejects the INSERT** and throws a foreign-key violation error. So the FK acts like a guard at the door: it makes "orphan" bookings (pointing to nothing) impossible. It also protects the other direction — you can't delete a match that still has bookings referencing it, so you never end up with bookings that suddenly point to a deleted match.

**One-line version:** A foreign key links `Bookings.match_id` to a real `Matches.match_id`, and the database refuses any booking whose match doesn't exist — that's referential integrity.

---

## Question 2 — Why can't we use `COUNT(booking_id)` inside a `WHERE` clause to filter rows? How does `HAVING` solve this?

It comes down to the **order in which SQL processes a query**. `WHERE` runs **early** — it filters individual rows *before* they are grouped, at a point where aggregate values like `COUNT`, `SUM`, or `AVG` haven't been calculated yet. An aggregate is a value computed *across a whole group of rows*, so asking `WHERE COUNT(...) > 2` is meaningless to the engine — at the `WHERE` stage there are no groups and no counts to compare against, so it raises an error.

`HAVING` exists exactly for this. It runs **after** `GROUP BY` has formed the groups and the aggregates have been computed, so it can filter those grouped results. The mental model is:

- `WHERE` filters **individual rows** (before grouping).
- `HAVING` filters **groups** (after grouping/aggregation).

**Example:** "show matches that have more than 2 bookings" →
`SELECT match_id, COUNT(booking_id) FROM Bookings GROUP BY match_id HAVING COUNT(booking_id) > 2;`

**One-line version:** `WHERE` runs before grouping so aggregates don't exist yet; `HAVING` runs after grouping, which is why it can filter on `COUNT`.

---

## Question 3 — If a Primary Key already guarantees every row is unique, why is it also forbidden from being `NULL`?

A Primary Key has **two** rules, not one: every value must be **unique**, *and* every value must be **NOT NULL**. They solve different problems.

`NULL` in SQL doesn't mean "empty" — it means **"unknown / no value."** The whole point of a primary key is to be a reliable **identifier** you can use to find exactly one row and to link other tables to it (via foreign keys). If a primary key could be `NULL`, you'd have a row whose identity is *unknown* — you couldn't reliably point a foreign key at it, and you couldn't tell two "unknown" rows apart, because in SQL `NULL` is never even considered equal to another `NULL`. That breaks the guarantee that a PK identifies exactly one specific row.

So uniqueness alone isn't enough: a key also has to **always be present** to do its job of identifying and being referenced.

**One-line version:** `NULL` means "unknown," and you can't identify a row or point a foreign key at an unknown value — so a primary key must be both unique *and* never null.

---

## Question 4 — In a `LEFT JOIN` of Users (left) to Bookings (right), what do the rows look like for a fan who has never booked?

A `LEFT JOIN` keeps **every row from the left table** (`Users`) whether or not it finds a match on the right (`Bookings`). For a brand-new fan with no bookings, the database still outputs **one row** for that fan — their `Users` columns (like `user_id` and `full_name`) are filled in normally, but **every column that comes from the `Bookings` side is `NULL`**, because there was nothing to match.

In our data this is exactly **Jannat Ara (user_id 4)** in Query 5: she appears in the result with her name, and `booking_id` shows up as `NULL`. That's the signature of "exists on the left, no match on the right." (If we'd used an `INNER JOIN` instead, she would disappear from the results entirely — which is why `LEFT JOIN` is the right choice when you want to keep users who haven't booked.)

**One-line version:** The fan still appears once, with their user details present and all booking columns showing `NULL` — like Jannat Ara with a `NULL` booking_id.

---

## Question 5 — What is the difference between a main query and a subquery, and when would you pick a subquery over a JOIN?

The **main (outer) query** is the primary statement that produces the final result. A **subquery** is a smaller query nested *inside* it — usually in parentheses — that runs first and hands its result up to the outer query to use. In Query 6 of this assignment, `(SELECT AVG(total_cost) FROM Bookings)` is a subquery: it calculates the average cost once, and the outer query compares each booking against that single value.

**When to prefer a subquery over a JOIN:**
- When you need a **single computed/aggregated value to compare against** (like an average, max, or count) — `WHERE total_cost > (SELECT AVG(...))` reads very naturally.
- When you're checking **existence or membership** rather than combining columns — e.g. `WHERE user_id IN (SELECT ...)` or `WHERE EXISTS (SELECT ...)`.
- When you don't actually want the other table's columns in your output — you only want to *filter* by it. A JOIN would multiply/duplicate rows and pull in columns you don't need.

A **JOIN** is the better tool when you genuinely need to **combine columns from multiple tables in the output** (like Query 4, showing the booking, the user's name, and the fixture together). Rough rule: **JOIN to combine data, subquery to filter by a derived/aggregated value.**

**One-line version:** A subquery is a query nested inside the main query that feeds it a value; use a subquery when you only need to filter by a computed value (like an average), and a JOIN when you actually need columns from both tables in the result.
