####
Para
####

.. image:: https://odkr.codeberg.page/para/_static/coverage.svg
   :target: https://odkr.codeberg.page/para/_static/coverage.html
   :alt: Coverage data

.. image:: https://www.bestpractices.dev/projects/9357/badge
   :target: https://www.bestpractices.dev/en/projects/9357
   :alt: OpenSSF best practices badge

Para is a command-line utility that runs jobs in parallel.

It is simpler, more lightweight, and more portable than
Concurrently_, `GNU Parallel`_, and rust-parallel_.
It's fast, too.

Para consists of a single source file, is written in C99_, only depends on
the C standard library, and compiles with ``-Wall -Wextra -Werror``. It
should work on almost every Unix-like system and is easy to integrate into
C-based projects.


Examples
========

Run ``echo foo`` and ``echo bar`` in parallel::

    $ para 'echo foo' 'echo bar'
    bar
    foo

Suppress job output, but show which jobs have been started::

    $ para -sv 'echo foo' 'echo bar'
    para: [31744] echo foo
    para: [31747] echo bar
    para: 2 jobs completed

Continue even though ``false`` exits with a non-zero status::

    $ para -c 'false' 'echo foo' 
    para: false[31744] exited with status 1
    foo

Add ``foo=bar`` and ``baz=qux`` to the job environment::

    $ para foo=bar baz=qux "sh -c 'echo \$foo'" "sh -c 'echo \$baz'"
    bar
    qux

Colorize output:

.. code:: bash

    blue="$(tput setaf 4)" cyan="$(tput setaf 6)" reset="$(tput sgr0)"
    para 'foo qux' 'bar quux' |
    sed "
      s/\(^foo:\)\(.*\)/$blue\1$reset\2/;
      s/\(^bar:\)\(.*\)/$cyan\1$reset\2/;
    "

Rename files from ``{x}.foo`` to ``{x}.bar``:

.. code:: bash

    find . -name '*.foo'              |
    # Escape meta-characters in filenames
    sed "s/\\(['\"\\\\]\\)/\\\\\\1/g" |
    while read -r file
    do printf 'mv "%s" "%s"\0' "$file" "${file%.foo}.bar"
    done                              |
    xargs -0 -n256 para

If no filename contains meta-characters
(i.e., '"', "'", and "\\"):

.. code:: bash

    for file in *.foo
    do printf 'mv "%s" "%s"\0' "$file" "${file%.foo}.bar"
    done |
    xargs -0 -n256 para

Requirements
============

Para should work on almost every Unix-like system. More precisely, it
should work on any system that complies with POSIX.1-2008_, including the
X/Open System Interface and Spawn extensions, and is compatible with
4.4BSD_.

Compiling Para requires:

* A C compiler that supports C99_
  (e.g., GCC_ ≥ v4.3 or Clang_ ≥ v1.0)
* An assembler and a linker
  (e.g., from `GNU Binutils`_ or a BSD system)
* Make (`GNU Make`_ and BSD makes are known to work)
* The header files of your system's standard library

Para comes with a script that installs
these dependencies if needed.

Installation
============

See ``INSTALL.rst``.


Documentation
=============

See the `home page`_, the manual_, and ``para -h``.


Contact
=======

Home page:
    https://odkr.codeberg.page/para

Issue tracker:
    https://github.com/odkr/para/issues

Source code (primary):
    https://codeberg.org/odkr/para

Source code (secondary):
    https://notabug.org/odkr/para

The GitHub repository only hosts discussions and the issue tracker.


License
=======

Copyright 2023 and 2024  Odin Kroeger

Para is free software: you can redistribute it and/or modify it
under the terms of the GNU General Public License as published by
the FreeSoftware Foundation, either version 3 of the License,
or (at your option) any later version.

Para is distributed in the hope that it will be useful, but WITHOUT
ANY WARRANTY; without even the implied warranty of MERCHANTABILITY
or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public
License for more details.

You should have received a copy of the GNU General Public License
along with Para. If not, see <https://www.gnu.org/licenses/>.

.. _4.4BSD: https://docs-legacy.freebsd.org/44doc/
.. _C99: https://en.cppreference.com/w/c/99
.. _Concurrently: https://github.com/open-cli-tools/concurrently
.. _Clang: https://clang.llvm.org/
.. _GCC: https://gcc.gnu.org/
.. _`GNU Binutils`: https://www.gnu.org/software/binutils/
.. _`GNU Make`: https://www.gnu.org/software/make/
.. _`GNU Parallel`: https://www.gnu.org/software/parallel/
.. _`home page`: https://odkr.codeberg.page/para
.. _manual: https://odkr.codeberg.page/para/manual
.. _POSIX.1-2008: https://pubs.opengroup.org/onlinepubs/9699919799.2008edition/
.. _rust-parallel: https://github.com/aaronriekenberg/rust-parallel
