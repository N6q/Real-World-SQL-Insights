# Real World SQL Insights

A comprehensive guide to understanding SQL usage in real-world applications, including cascading actions, DQL in major platforms, and data fetching strategies in scrolling interfaces.

---

## 📑 Table of Contents

* [Foreign Key Cascading](#foreign-key-cascading)
* [DQL in Action](#dql-in-action)
* [Is Scrolling in Apps Powered by SQL?](#is-scrolling-in-apps-powered-by-sql)

---

## 📌 Foreign Key Cascading

### ON DELETE CASCADE

The `ON DELETE CASCADE` action in Postgres automatically deletes related rows in child tables when a parent row is deleted, maintaining referential integrity in the database. (Gyamfi, n.d.)

**Implementation Example:**

```sql
CREATE TABLE parent_table(
    id SERIAL PRIMARY KEY
);

CREATE TABLE child_table(
    id SERIAL PRIMARY KEY,
    parent_id INT,
    FOREIGN KEY(parent_id) REFERENCES parent_table(id) ON DELETE CASCADE
);
```

### ON UPDATE CASCADE

The `ON UPDATE CASCADE` option applies when the primary key in the parent table is updated, ensuring that corresponding foreign key values in child tables are also updated. (Prasad, 2024)

**Implementation Example:**

```sql
CREATE TABLE parent_table (
    parent_id INT PRIMARY KEY
);

CREATE TABLE child_table (
    child_id INT PRIMARY KEY,
    parent_id INT,
    FOREIGN KEY (parent_id) REFERENCES parent_table(parent_id) ON UPDATE CASCADE
);
```

### Potential Risks of Cascading Deletes:

* Accidental Data Loss
* Complexity
* Performance Issues
* Maintenance Challenges
* Transaction Conflicts
* Data Integrity Risks
* Debugging Difficulty (Beckett, 2020)

---

## 📌 DQL in Action

### How Platforms Use SELECT Queries:

* **Amazon:** Product search, order history, inventory management.
* **Netflix:** Content recommendations, watch history, trending content.
* **Banking Apps:** Account balance, transaction history, loan details.

### Data Retrieval Frequency:

* **Amazon:** Real-time data for product listings and orders.
* **Netflix:** Continuous data retrieval for recommendations.
* **Banking Apps:** On-demand data access for transactions.

### Where DQL Fits in Daily Operations:

* Real-Time Data Retrieval
* Personalization
* Operational Efficiency

**Bonus Insight:**
In Spotify, SELECT queries retrieve a user's listening history and preferences to generate personalized playlists and song recommendations.

---

## 📌 Is Scrolling in Apps Powered by SQL?

### How Scrolling Works Behind the Scenes:

* SELECT queries fetch the next set of data as the user scrolls.

**Example:**

```sql
SELECT * FROM products ORDER BY popularity DESC LIMIT 20 OFFSET 40;
```

### Fetching More Data:

* **LIMIT and OFFSET:**

  ```sql
  SELECT * FROM items ORDER BY created_at DESC LIMIT 10 OFFSET 30;
  ```

* **Cursor-Based Pagination:**

  ```sql
  SELECT * FROM items WHERE id > last_seen_id ORDER BY id ASC LIMIT 10;
  ```

### Pagination and Lazy Loading:

* **Pagination:** Fetches specific data sets per page.
* **Infinite Scrolling:** Loads additional content as the user scrolls.
* **Lazy Loading:** Delays data retrieval until needed, reducing load times.

**Bonus Insight:**
In Spotify, SELECT queries load song information in batches, ensuring quick load times and a seamless user experience.

---

## 📦 Resources

* [PostgreSQL Documentation - CASCADE](https://www.postgresql.org/docs/current/ddl-constraints.html)
* [GeeksforGeeks - SQL Pagination](https://www.geeksforgeeks.org/sql-pagination/)
* [Spotify Developer Documentation](https://developer.spotify.com/documentation/)
