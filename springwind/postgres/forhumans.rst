Postgres for Humans
===================

Source: https://www.youtube.com/watch?time_continue=80&v=MpH8W5hce9I

Learn:

* Datatypes
* Conditional Indexes
* Transactional DDL
* Foreign Data Wrappers
* Concurrent Index Creation
* Extensions
* Common Table Expression
* Fast Column Addition
* Listen / Notify
* Table Inheritance
* Per Transaction sync replication
* Window Function
* NoSQL inside SQL
* Momentum

OLTP vs OLAP
------------
**OLTP** equals mostly webapps. **OLAP** mostly equals business intelligence
and reporting.


Setup / Config
--------------
-> Talk Postgresql when it is not your day job.


Cache all the things
--------------------
PostgreSQL is very good in caching your data.
If you do not have a cache hit rate of 99%
you should add more memory to the box.
Try to get a cache hit rate of 99%::

    SELECT 
      sum(heap_blks_read) as heap_read,
      sum(heap_blks_hit)  as heap_hit,
      sum(heap_blks_hit) / (sum(heap_blks_hit) + sum(heap_blks_read)) as ratio
    FROM 
      pg_statio_user_tables;
        

Index Hit Rate
--------------
Should be greater than 95%.
Asks how often you use indexes to query the database::

    SELECT 
      relname, 
      100 * idx_scan / (seq_scan + idx_scan) percent_of_times_index_used, 
      n_live_tup rows_in_table
    FROM 
      pg_stat_user_tables
    WHERE 
        seq_scan + idx_scan > 0 
    ORDER BY 
      n_live_tup DESC;
      
You can try as well this query::

    SELECT
        relname,
        100 * idx_scan / (seq_scan + idx_scan),
        n_live_tup
    FROM pg_stat_user_tables
    ORDER BY n_live_tup DESC;
    
    
Use a `.psqlrc` file
--------------------
For example to define a function::

    \set show_slow_queries
    'SELECT
    (total_time / 1000 / 60) as total_minutes,
    (total_time/calls) as average_time, query
    FROM pg_stat_statements
    ORDER BY 1 DESC
    LIMIT 100;'    
    

Understand specific query performance
-------------------------------------
You always can put an `EXPLAIN` in front of a SQL
query and `EXPLAIN_ANALYZE` to get the real 
time of a query. You are mostly interested in the
**max** time in the analysis::

    actual time=startuptime..maxtime rows=1000
      
Common response times:
* Page Response time <100ms
* Common queries <10ms ==> aim at around 1ms
* Rare queries <100ms

This helps you to find locations where to put indexes::

    CREATE INDEX idx_emps ON employees (salary);
    

pg_stat_statements
------------------
   
