Postgres and Django ORM Basics
==============================

The Django ORM is not always the most efficient and ideal way to access
data in the database. It should be focused on **CRUD** applications (Create, Read, Update, Delete).

* **READ**: The ORM is useful if you need to read a whole row on a single table. If you
however need only IDs or a subset of columns or complicated joined tables - you should consider
to use SQL directly if the query is a bottleneck.