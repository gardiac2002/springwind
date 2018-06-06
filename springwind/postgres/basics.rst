Postgres and Django ORM Basics
==============================

Postgres: Table sizes
---------------------


General table size information
******************************

.. code-block:: sql

	SELECT *, pg_size_pretty(total_bytes) AS total
		, pg_size_pretty(index_bytes) AS INDEX
		, pg_size_pretty(toast_bytes) AS toast
		, pg_size_pretty(table_bytes) AS TABLE
	  FROM (
	  SELECT *, total_bytes-index_bytes-COALESCE(toast_bytes,0) AS table_bytes FROM (
		  SELECT c.oid,nspname AS table_schema, relname AS TABLE_NAME
		          , c.reltuples AS row_estimate
		          , pg_total_relation_size(c.oid) AS total_bytes
		          , pg_indexes_size(c.oid) AS index_bytes
		          , pg_total_relation_size(reltoastrelid) AS toast_bytes
		      FROM pg_class c
		      LEFT JOIN pg_namespace n ON n.oid = c.relnamespace
		      WHERE relkind = 'r'
	  ) a
	) a;


Finding the size of your biggest relations
******************************************

.. code-block:: sql

	SELECT nspname || '.' || relname AS "relation",
		pg_size_pretty(pg_relation_size(C.oid)) AS "size"
	  FROM pg_class C
	  LEFT JOIN pg_namespace N ON (N.oid = C.relnamespace)
	  WHERE nspname NOT IN ('pg_catalog', 'information_schema')
	  ORDER BY pg_relation_size(C.oid) DESC
	  LIMIT 20;


Finding the total size of your biggest tables 
*********************************************

.. code-block:: sql

	SELECT nspname || '.' || relname AS "relation",
		pg_size_pretty(pg_total_relation_size(C.oid)) AS "total_size"
	  FROM pg_class C
	  LEFT JOIN pg_namespace N ON (N.oid = C.relnamespace)
	  WHERE nspname NOT IN ('pg_catalog', 'information_schema')
		AND C.relkind <> 'i'
		AND nspname !~ '^pg_toast'
	  ORDER BY pg_total_relation_size(C.oid) DESC
	  LIMIT 20;




The Build: Blog
---------------

http://thebuild.com/blog/


The Django ORM :: limitations
-----------------------------


The Django ORM is not always the most efficient and ideal way to access
data in the database. It should be focused on **CRUD** applications (Create, Read, Update, Delete).

* **READ**: The ORM is useful if you need to read a whole row on a single table. If you
however need only IDs or a subset of columns or complicated joined tables - you should consider
to use SQL directly if the query is a bottleneck.




