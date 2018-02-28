

Celery Basics
=============


Automatic Retrying of Tasks and time increase
---------------------------------------------

Celery tasks my fail - so you should retry failing tasks
if necessary: http://docs.celeryproject.org/en/latest/userguide/tasks.html#retrying

In the best case, the retry waiting time should increase over time
in order to avoid system flooding:

Source: https://medium.com/@taylorhughes/three-quick-tips-from-two-years-with-celery-c05ff9d7f9eb

.. code-block:: python

    @celery_app.task(max_retries=10)
    def notify_gcm_device(device_token, message, data=None):
      notification_json = build_gcm_json(message, data=data)

      try:
        gcm.notify_device(device_token, json=notification_json)

      except ServiceTemporarilyDownError:
        # Find the number of attempts so far
        num_retries = notify_gcm_device.request.retries
        seconds_to_wait = 2.0 ** num_retries

        # First countdown will be 1.0, then 2.0, 4.0, etc.
        raise notify_gcm_device.retry(countdown=seconds_to_wait)


Worker configuration
--------------------

Autoscaling
***********

Allows to scale celery workers depending on activity.
This decreases the load of your system in times of inactivity:

::

    --autoscale=16,4

This configuration scales maximally to 16 workers (= 16 cores) and always
keeps at least 4 workers.

.. important:: It is recommended


Use -Ofair for preforking workers
*********************************
If you have a set of tasks that take varying amounts of time to complete — either
deliberately or due to unpredictable network conditions, etc. — this will cause
unexpected delays in total execution time for tasks in the queue.


A global task timeout
*********************
Tasks might get blocked for an infinite time.
So you might consider to add a global task timeout in your `settings.py`:

.. code-block:: python

    CELERYD_TASK_SOFT_TIME_LIMIT = 60

