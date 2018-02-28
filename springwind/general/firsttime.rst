Building a reasonably popular web application
=============================================

Source: https://www.youtube.com/watch?v=aFlKpLMrM0c


Recommendations
---------------

* **Aggregate logs** and monitor from day 1. Moreover keep your logs
  clean and react to bad log messages.

* **Profile**: Have a way to profile your API calls! (e.g. **Django-Silk**).
  Maybe add a profiling flag to the REST API for introspection.  

* **Know when things fail**: Add job expectations and job results as a
  concept.

* **Have a way to keep secrets**: From the beginning e.g. with **ansible vault**.

* **Everything needs a limit**: Throttling, request limits,  

* **Plan for database downtime**: 

* **Have a way to go into maintenance mode**

* **Use feature flags** for partial rollouts.
