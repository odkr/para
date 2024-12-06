[![OpenSSF best practices badge](https://www.bestpractices.dev/projects/9357/badge)](https://www.bestpractices.dev/en/projects/9357 )

# Para

Para is a command-line utility that runs jobs in parallel.

It is simpler, lighter, and more portable than
[Concurrently](https://github.com/open-cli-tools/concurrently),
[GNU Parallel](https://www.gnu.org/software/parallel/), and
[rust-parallel](https://github.com/aaronriekenberg/rust-parallel).

It consists of a single source file, is written in [C99](https://en.cppreference.com/w/c/99),
and only uses the Unix standard library. So it should work on almost every Unix-like system and
be easy to integrate into C-based projects.

It's fast, too.

> [!IMPORTANT]  
> The GitHub repository only hosts [discussions](https://github.com/odkr/para/discussions)
> and the [issue tracker](https://github.com/odkr/para/issues).
> 
> * [Download Para](https://odkr.codeberg.page/para/install.html)
> * [Get the source code](https://codeberg.org/odkr/para)


## Examples

Run **echo foo** and **echo bar** in parallel:

```
$ para 'echo foo' 'echo bar'
bar
foo
```

Compose commands from arguments:

```
$ para -c 'echo {}' foo bar baz
foo
bar
baz
```

Add ``FOO=bar`` and ``BAZ=qux`` to the job environment:

```
$ para FOO=bar 'sh -c "echo $FOO"'
bar
```

## Requirements

Para should work on almost every Unix-like system. More precisely, it should work on every system
that complies with [POSIX.1-2008](https://pubs.opengroup.org/onlinepubs/9699919799.2008edition/),
including the X/Open System Interface and Spawn extensions. It has been tested on Alpine Linux,
Debian, Darwin, FreeBSD, NetBSD, and OpenBSD.

Compiling Para requires:

* A C compiler that supports C99_
  (e.g., [GCC](https://gcc.gnu.org/) ≥ v4.3,
         [Clang](https://clang.llvm.org/) ≥ v1.0, or
         [TinyCC](http://tinycc.org/) ≥ v0.9)
* An assembler and a linker
  (e.g., from [GNU Binutils](https://www.gnu.org/software/binutils/) or a BSD system)
* Make ([GNU Make](https://www.gnu.org/software/make/) and BSD makes are known to work)
* The header files of your system's standard library

Para comes with a script that installs
these dependencies if needed.


## Installation

See <https://odkr.codeberg.page/para/install>


## Documentation

See the [home page](https://odkr.codeberg.page/para), the
[manual](https://odkr.codeberg.page/para/manual), and **para -h**.


## Contact

Home page: <https://odkr.codeberg.page/para>

Issue tracker: <https://github.com/odkr/para/issues>

Source code (primary): <https://codeberg.org/odkr/para>

Source code (mirror): <https://repo.or.cz/para.git>

The GitHub repository only hosts discussions and the issue tracker.


## License

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
