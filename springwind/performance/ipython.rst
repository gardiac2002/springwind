IPython Performance Measuring
=============================

An easy solution to profiling the CPU
and memory needs of your application are the following
**IPython** *magic* methods:

* `%time` & `%timeit`: See how long a script takes to run (one time, or averaged over a bunch of runs).
* `%prun`: See how long it took each function in a script to run.
* `%lprun`: See how long it took each line in a function to run.
* `%mprun` & `%memit`: See how much memory a script uses (line-by-line, or averaged over a bunch of runs).

In order to use the various profilers you need to install the following requirements:

::

    $ pip install line-profiler
    $ pip install psutil
    $ pip install memory_profiler

Moreover, in your **IPython** session run the following code before using the wished
profiler:

.. code-block:: python

    %load_ext line_profiler
    %load_ext memory_profiler

