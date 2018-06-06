

Django Performance Basics
=========================


Prepared statements
-------------------
If you want to access database prepared statements:

.. code-block:: python


    from django.db import connections

    with connection.cursor() as cursor:
        cursor.callproc('test_procedure', [1, 'test'])


Useful plugins
--------------

* django-extensions
* django-debug-toolbar
* django-cacheops

::

    python manage.py runprofileserver --use-cprofile --prof-path=/tmp/profile_data/

create a graph:

::

    gprof2dot -f pstats mpyrofilefile.prof | dot -Tpng -o profile_graph.png