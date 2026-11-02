# SQL and Database Testing Notes with Example Queries

Practical notes for the database side of QA: what to check behind the UI and the SQL to check it with. The example queries below were actually executed (SQLite, 2 Nov 2026) against a small shop-style schema - products, users, orders - modeled on the practice app this portfolio uses. Outputs shown are the real results of that run.

## What database testing checks behind a web app

1. **CRUD through the UI lands correctly** - after adding/changing/deleting something in the UI, read the table and confirm the row matches (values, types, timestamps).
2. **Constraints hold** - NOT NULL, UNIQUE, CHECK and foreign keys reject bad data at the database level, not only in form validation. Test by trying to insert a violating row directly.
3. **Data integrity over time** - no orphans (orders pointing at deleted products), no duplicates in unique fields, no NULLs where the UI assumes a value.
4. **Calculations agree with the UI** - totals, tax and counts computed in SQL match what the page shows.

## Example schema used for the runs

```sql
CREATE TABLE products (id INTEGER PRIMARY KEY, name TEXT NOT NULL,
                       price REAL NOT NULL CHECK(price >= 0), stock INTEGER NOT NULL DEFAULT 0);
CREATE TABLE users (id INTEGER PRIMARY KEY, username TEXT UNIQUE NOT NULL, email TEXT);
CREATE TABLE orders (id INTEGER PRIMARY KEY, user_id INTEGER NOT NULL REFERENCES users(id),
                     product_id INTEGER NOT NULL REFERENCES products(id),
                     qty INTEGER NOT NULL CHECK(qty > 0), created_at TEXT NOT NULL);
```

## Worked queries (executed 2 Nov 2026, outputs are real)

Sort check - the UI's "Price (low to high)" should match the database order:

```sql
SELECT name, price FROM products ORDER BY price ASC;
-- ('Sauce Labs Onesie', 7.99) ('Sauce Labs Bike Light', 9.99) ('Sauce Labs Backpack', 29.99)
```

Inventory check - anything the UI sells that is actually out of stock:

```sql
SELECT name FROM products WHERE stock = 0;
-- ('Sauce Labs Bike Light',)
```

Join check - orders readable the way a support agent would ask about them:

```sql
SELECT u.username, p.name, o.qty
FROM orders o
JOIN users u ON u.id = o.user_id
JOIN products p ON p.id = o.product_id
ORDER BY o.created_at;
-- standard_user Backpack 2 | standard_user Onesie 1 | problem_user Backpack 1
```

Totals check - revenue per product, the kind of number a dashboard shows:

```sql
SELECT p.name, SUM(o.qty * p.price) AS revenue
FROM orders o JOIN products p ON p.id = o.product_id
GROUP BY p.name ORDER BY revenue DESC;
-- ('Sauce Labs Backpack', 89.97) ('Sauce Labs Onesie', 7.99)
```

Missing-data check - profiles the UI might choke on:

```sql
SELECT username FROM users WHERE email IS NULL;
-- ('problem_user',)
```

Duplicate check - a UNIQUE column should make this return nothing:

```sql
SELECT username, COUNT(*) AS n FROM users GROUP BY username HAVING n > 1;
-- (no rows)
```

Constraint check - a negative price must be rejected:

```sql
INSERT INTO products (name, price, stock) VALUES ('Bad', -5, 1);
-- rejected: CHECK constraint failed: price >= 0
```

## Notes on running database tests

- Run read-only queries (SELECT) against shared environments; write checks (INSERT/UPDATE) belong on disposable test data like the schema above.
- A UI test and a database check are stronger together: the UI test proves the flow works, the SQL proves the record behind it is right.
- When a UI bug is suspected to be data-driven (like the problem_user behaviors in bug-reports/saucedemo/), comparing the underlying rows between a working and a failing account is often the fastest way to localize it.
- SQLite runs the examples here with zero setup; the same queries work on MySQL/PostgreSQL with only date-function and type tweaks.
