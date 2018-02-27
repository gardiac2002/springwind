

Django Performance Basics
=========================


Useful plugins
--------------

* django-extensions
* django-debug-toolbar
* django-cacheops

python manage.py runprofileserver --use-cprofile --prof-path=/tmp/profile_data/
create a graph:
gprof2dot -f pstats mpyrofilefile.prof | dot -Tpng -o profile_graph.png