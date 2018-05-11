Maximal number of gunicorn workers
==================================

gunicorn -w $(( 2 * `cat /proc/cpuinfo | grep 'core id' | wc -l` + 1 )) myapp:wsgi
