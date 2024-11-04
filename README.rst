.. image:: https://www.bestpractices.dev/projects/9357/badge
   :target: https://www.bestpractices.dev/en/projects/9357
   :alt: OpenSSF best practices badge


####
Para
####

Para is a command-line utility that runs jobs in parallel.

It is simpler, more lightweight, and more portable than
Concurrently_, `GNU Parallel`_, and rust-parallel_.
It's fast, too.

Para comprises a single source file, is written in C99_, only uses the
Unix standard library, and compiles with :option:`-Wall -Wextra -Werror`.
It should work out-of-the-box on almost every Unix-like system and be
easy to integrate into C-based projects.

.. _C99: https://en.cppreference.com/w/c/99
.. _Concurrently: https://github.com/open-cli-tools/concurrently
.. _`GNU Parallel`: https://www.gnu.org/software/parallel/
.. _rust-parallel: https://github.com/aaronriekenberg/rust-parallel


Examples
========

Run **echo foo** and **echo bar** in parallel::

    $ para 'echo foo' 'echo bar'
    bar
    foo

Compose commands from arguments::

    $ para -k 'echo {}' foo bar baz
    foo
    bar
    baz

Add ``FOO=bar`` and ``BAZ=qux`` to the job environment::

    $ para FOO=bar BAZ=qux 'sh -c "echo $FOO"' 'sh -c "echo $BAZ"'
    bar
    qux


Requirements
============

Para should work on almost every Unix-like system. More precisely, it
should work on every system that complies with POSIX.1-2008_, including the
X/Open System Interface and Spawn extensions. It has been tested
on Alpine Linux, Debian, Darwin, FreeBSD, NetBSD, and OpenBSD.

Compiling Para requires:

* A C compiler that supports C99_
  (e.g., GCC_ ≥ v4.3, Clang_ ≥ v1.0, or TinyCC_ ≥ v0.9)
* An assembler and a linker
  (e.g., from `GNU Binutils`_ or a BSD system)
* Make (`GNU Make`_ and BSD makes are known to work)
* The header files of your system's standard library

Para comes with a script that installs
these dependencies if needed.

.. _Clang: https://clang.llvm.org/
.. _GCC: https://gcc.gnu.org/
.. _`GNU Binutils`: https://www.gnu.org/software/binutils/
.. _`GNU Make`: https://www.gnu.org/software/make/
.. _POSIX.1-2008: https://pubs.opengroup.org/onlinepubs/9699919799.2008edition/
.. _TinyCC: http://tinycc.org/


Installation
============

See **INSTALL.rst**.


Documentation
=============

See the `home page`_, the manual_, and **para -h**.

.. _`home page`: https://odkr.codeberg.page/para
.. _manual: https://odkr.codeberg.page/para/manual


Contact
=======

Home page:
    https://odkr.codeberg.page/para

Issue tracker:
    https://github.com/odkr/para/issues

Source code (primary):
    https://codeberg.org/odkr/para

Source code (mirror):
    https://repo.or.cz/para.git

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
