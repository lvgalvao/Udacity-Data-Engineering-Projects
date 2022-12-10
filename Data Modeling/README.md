# L1 Exercise 1 - Creating a table with postgres

# L1 Exercise 2 - Creating a table with cassandra using docker

To use 'cassandra-driver' needs python >3.8
To run exercise 2 needs to run cassandra on Docker following this commandas:

> docker run -d --name cassandra-node -p 9042:9042 cassandra

# L2 demo 1 - Creating normalized tables

*Normalization and Denormalization*

Normalization will feel like a natural process, you will reduce the number of copies of the data and increase the likelihood that your data is correct in all locations.

<li> Normalization organizes the columns and tables in a database to ensure that their dependencies are properly enforced by database integrity constraints.

<li> We don’t want or need extra copies of our data, this is data redundancy. We want to be able to update data in one place and have that be the source of truth, that is data integrity. 

*L2 demo 1 - Creating normalized tables* is an exercise to normalize table through all the necessary steps.

*Objectives of Normal Form:*

<li>To free the database from unwanted insertions, updates, & deletion dependencies
<li>To reduce the need for refactoring the database as new types of data are introduced
<li>To make the relational model more informative to users
<li>To make the database neutral to the query statistics

See this [Wikipedia](https://en.wikipedia.org/wiki/Database_normalization) page to learn more.

*How to reach First Normal Form (1NF):*

 <li>Atomic values: each cell contains unique and single values
 <li>Be able to add data without altering tables
 <li>Separate different relations into different tables
 <li>Keep relationships between tables together with foreign keys

*Second Normal Form (2NF):*

<li>Have reached 1NF
<li>All columns in the table must rely on the Primary Key

*Third Normal Form (3NF):*

 <li>Must be in 2nd Normal Form
 <li> No transitive dependencies

*When to use 3NF:*

When you want to update data, we want to be able to do in just 1 place.

# L2 demo 2 - Creating normalized tables

JOINS on the database allow for outstanding flexibility but are extremely slow. If you are dealing with heavy reads on your database, you may want to think about denormalizing your tables. You get your data into normalized form, and then you proceed with denormalization. So, denormalization comes after normalization.