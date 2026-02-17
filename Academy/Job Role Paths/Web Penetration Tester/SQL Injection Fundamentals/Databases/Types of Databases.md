# Types of Databases

Databases are categorized into **Relational** and **Non-Relational** types. Only Relational Databases use SQL, while Non-Relational databases use various communication methods.

## Relational Databases

A relational database uses a **schema** (template) to structure stored data. For example, a company selling products might use three tables:
- Customer information
- Products and costs
- Orders with payment data

### Keys and Relationships

Tables use **keys** to provide quick access to specific rows or columns. Each customer gets a unique ID linking to their address, name, and contact info. Similarly, each product has an ID. Orders only need to store these IDs and quantities.

### RDBMS Concept

A **Relational Database Management System (RDBMS)** links tables using keys. Many companies now use RDBMS due to its simplicity. Examples include MySQL, SQL Server, Oracle, and PostgreSQL.

**Example Structure:**
- `users` table: id, username, first_name, last_name
- `posts` table: id, user_id, date, content

By linking `user_id` in posts to `id` in users, you can retrieve user details without duplicating data.

### Benefits

Relational databases enable fast, reliable retrieval of all data about a specific element across multiple tables with a single query. This makes them ideal for large, well-structured datasets.

## Non-Relational Databases

**NoSQL databases** don't use tables, rows, columns, or schemas. They store data using various models and are highly scalable and flexible for unstructured data.

### Common Storage Models

1. **Key-Value** - Stores data as key-value pairs (JSON/XML)
2. **Document-Based** - Document-oriented storage
3. **Wide-Column** - Column-oriented storage
4. **Graph** - Graph-based storage

### Example: Key-Value Model

```json
{
    "100001": {
        "date": "01-01-2021",
        "content": "Welcome to this web application."
    },
    "100002": {
        "date": "02-01-2021",
        "content": "This is the first post on this web app."
    }
}
```

Similar to Python/PHP dictionaries, where the key is usually a string and the value can be any type.

### NoSQL Injection

NoSQL databases use a different injection method called **NoSQL injection**, which differs from SQL injection and will be covered in a later module.

**Common example:** MongoDB
