Build
=====

Install a C build toolchain::

    sudo ./installc

Detect the build configuration::

    ./configure

Build Para::

    make

See :doc:`build` for details and troubleshooting.


Installation
============

Install Para *either* system-wide::

    sudo make install

*Or* to your home directory::

    make prefix=~/.local install


De-installation
===============

.. code:: bash

    sudo make uninstall

.. tip::
    If Para was installed to a directory you have write permissions for,
    :command:`make uninstall` suffices.
