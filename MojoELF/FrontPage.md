# MojoELF 1.0

The latest version of this library is available from [GitHub](https://github.com/icculus/mojoelf).

A detailed overview, and a list of available APIs, can be viewed in [CategoryMojoELF](CategoryMojoELF).

MojoELF is an ELF binary loader that runs in your application instead of as part of the C runtime.
Its most useful feature is that, unlike the standard `dlopen()`, it can load an ELF file from a place
other than the filesystem. Notably, it can load one from a buffer in memory.

It is available under the zlib license, found in the file [LICENSE.txt](https://github.com/icculus/mojoelf/blob/main/LICENSE.txt).

Enjoy!

