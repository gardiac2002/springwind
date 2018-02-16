

Installation
============


Prerequirements
---------------

* npm
* node

IJavascript Installation
------------------------

    >>> sudo apt-get install nodejs-legacy npm ipython ipython-notebook
    >>> sudo npm install -g ijavascript
    >>> ijsinstall


Haskell Installation
--------------------

    >>> sudo add-apt-repository ppa:chronitis/jupyter
    >>> sudo apt-get update
    >>> sudo apt-get install ihaskell


NodeJS Installation
-------------------

    >>> git clone https://github.com/notablemind/jupyter-nodejs.git
    >>> cd jupyter-nodejs
    >>> mkdir -p ~/.ipython/kernels/nodejs/
    >>> npm install && node install.js
    >>> npm run build
    >>> npm run build-ext
    >>> jupyter console --kernel nodejs