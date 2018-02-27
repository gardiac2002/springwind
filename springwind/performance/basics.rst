Profiling Basics
==================


**Early optimization is the root of all evil**

Optimization should be done before thinking about distributing your
application or dividing it up in micro services. Many developers
try to guess where an application might be slower or faster. 
Better profile your app!


CPU Profiling
-------------

Many people focus on local optimizations. But a focus on
bottlenecks is more useful. The standard profiling tool
is `cProfile`:

.. code-block:: python

    import cProfile
    cProfile.run('1 + 1')
    

It is easier to use `cProfile` directly with a script:

::

   python3 -m cProfile script.py
    
In order to better understand the program performance we 
should make it readable for **KCacheGrind**. The program
**pyprof2calltree** can convert the data format of `cProfile` 
to a **KCacheGrind** profile:

::

    python3 -m cProfile -o script_performance.cprof script.py
    pyprof2calltree -k -i script_performance.cprof
    
If you do not like **KCacheGrind** you might use **RunSnake**:

::

    python3 -m cProfile -o script_performance.cprof script.py
    runsnake script_performance.cprof 
    
.. important:: Full code profiling runs might eat up a huge amount of memory. Consider to profile selected unit tests.


Memory Profiling
----------------

The package `memory-profiler` allows us to understand the used memory better.
Annotate the target function with the `@profile` annotation.
Then you can run the code with:

::

    python3 -m memory_profiler script.py


Memory Views
------------

If your program needs too much memory you might consider to use
the buffer protocol (PEP 3118) and `memoryview`. Thanks to `memoryview` you
don't need to copy the can be looked up directly.