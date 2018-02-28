Django on Steroids 
==================

Source: https://www.youtube.com/watch?v=E5JQlHLimTA


Tuning your WSGI
----------------

* Use `Gunicorn`!
* Introspect what your application is doing:

  - IO intensive ?
  - memory intensive ? 

* Determine `worker_class`. Know when to use `sync` and `async` workers.
  For normal traffic `sync` mode works pretty well. `async`-mode is very 
  useful if you talk to many other applications (with various response
  times). Consider to use `gevent` for `async` code.

* Adjust params like `workers`, `worker_connections` and `keepalive`.
  Requests might be dropped between **nginx** and **gunicorn**. Take
  a look at the `keepalive` option.

* There is no such thing as too many workers -> **wrong**. Usually,
  6 - 12 gunicorn workers are enough to handle around 100.000 requests.
  If you require more than 12 workers you probably should scale 
  horizontally (-> more hosts!).


Tune the proxy server (nginx)
-----------------------------

* Use **nginx**.
* `worker_processes auto;`: Default configuration is `1`. Better use `auto`.
  This scales automatically to the number of cores to the machine.
* Adjust `keepalive_timeout` depending on `gunicorn`.
* Turn on `tcp_nopush` and `tcp_nodelay`. Useful when you host an API server
  with numerous small requests.
* `gzip` all the things!
* **Measure everything you can!**


What is taking so long?
-----------------------

* Use Chrome Dev Tools to find out the rate-limiting step.
* `EXPLAIN_ANALYZE` for complex queries.
* Python often is not a performance bottleneck.
* Use caching often and intelligently.
* `tail` your database logs.


Caching
-------

* Use **redis**.
* Use **Redis** as your primary cache. Cache very often:
  
  * All user sessions.
  * `User` model lookups.
  * Resource-level caching

* Use a CDN for all the things which cannot be changed by the user:

  * static files
  * images, etc.


Django ORM
----------
The Django ORM is powerful, but not always the best tool. Break away
when necessary:

* Tail your database logs.
* Automatic relationships can be very dangerous. Expand them
  carefully.
* Add extra indices if necessary.
* Heavy lifting should be done at the database when possible.






