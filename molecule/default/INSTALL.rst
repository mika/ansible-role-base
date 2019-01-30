*******
Docker driver installation guide
*******

Requirements
============

* General molecule dependencies (see https://molecule.readthedocs.io/en/latest/installation.html)
* Docker Engine
* docker-py

Install
=======

    $ virtualenv $HOME/venv
    $ source $HOME/venv/bin/activate
    $ pip install ansible molecule docker-py

Usage
=====

If you have apt-cacher-ng running, set the http_proxy variable:

    $ export http_proxy=http://172.17.0.1:3142/

To run the tests run:

    $ molecule test
