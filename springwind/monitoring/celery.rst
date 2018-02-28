
Celery Monitoring
=================

There are an array of monitoring possibilities for celery:

* **stats** requests celery statistics as a JSON.
* **flower** is a celery monitoring web application.
* **rabbitmqctl** for RabbitMQ controls and statistics.


Celery stats
------------
Source: http://docs.celeryproject.org/en/latest/userguide/workers.html#worker-statistics

Access the worker statistics through the command

::

    celery -A <project-name> inspect stats


In the returned JSON the `rusage` is particularly informative.
Take a look the the metrices:

* `maxrss`: The maximum resident/real size used by this process (in kilobytes).
* `inblock`: Number of times the file system had to read from the disk on behalf of this process.


Flower
------

Run with the command `flower -A <project-name> --port=5555` and access the data through
the web browser at port 5555.



RabbitMQCtl
-----------

To access the memory data of the queues use

::

    sudo rabbitmqctl list_queues name memory

