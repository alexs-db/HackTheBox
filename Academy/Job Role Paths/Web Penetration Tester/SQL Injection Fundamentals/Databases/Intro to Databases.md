# Intro to Databases

Before learning about SQL injections, we must understand databases and Structured Query Language (SQL). Web applications use back-end databases to store content, files, posts, and user data like usernames and passwords.

Different database types serve different purposes. File-based databases became inefficient as data grew, leading to the adoption of Database Management Systems (DBMS).

## Database Management Systems

A **DBMS** creates, defines, hosts, and manages databases. Various types exist: file-based, Relational (RDBMS), NoSQL, Graph-based, and Key/Value stores.

You can interact with a DBMS through command-line tools, graphical interfaces, or APIs. DBMS is widely used in banking, finance, and education. Essential features include:

| Feature | Description |
|---------|-------------|
| **Concurrency** | Handles multiple simultaneous users without data corruption or loss |
| **Consistency** | Ensures data remains valid throughout concurrent interactions |
| **Security** | Provides user authentication and permissions for data protection |
| **Reliability** | Enables backup and rollback capabilities |
| **SQL** | Offers intuitive syntax for various database operations |

## Architecture

A typical three-tier architecture consists of:

- **Tier I**: Client-side applications (websites, GUI programs) handling user interactions
- **Tier II**: Middleware that interprets events and formats them for the DBMS
- **Tier III**: DBMS that processes queries (insert, retrieve, delete, update) and returns results

While the application server and DBMS can be hosted together, large-scale systems typically separate them for better performance and scalability.
