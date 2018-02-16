

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


Rust installation
-----------------
Unfortunately, Rust does not work yet. :(

    >>> sudo apt update && sudo apt -y install curl
    >>> curl -sSf https://static.rust-lang.org/rustup.sh | sh

    >>> # Check installation
    >>> rustc -V
  
    >>> sudo apt install libzmq3-dev
    >>> cd $HOME
    >>> git clone https://github.com/pwoolcoc/jupyter-rs.git
    >>> cd jupyter-rs
    >>> cargo build --release
    
    # Potential Error
    # error[E0554]: #![feature] may not be used on the stable release channel
    # Solution
    >>> rustup override set nightly
    >>> cargo build --release
    >>> ./setup.sh
    
    
    
