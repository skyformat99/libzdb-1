# Libzdb

[![Build Status](https://travis-ci.org/taka-wang/libzdb.svg?branch=master)](https://travis-ci.org/taka-wang/libzdb)
[![Platform](https://img.shields.io/badge/platform-linux%7Cmac-lightgrey.svg)](https://github.com/taka-wang/libzdb)
[![License](https://img.shields.io/badge/license-GPLv3-blue.svg)](https://raw.githubusercontent.com/taka-wang/libzdb/master/COPYING)

## Introduction

 Libzdb is a database library with thread-safe connection pooling. The
 library can connect transparently to multiple database systems. It has
 zero runtime configuration and connection is specified via a URL scheme.

![model](model.png "Model")

## System requirements

- Memory and Disk space

   A minimum of 1 megabytes RAM are required and around 700KB of free
   disk space. You may need more RAM depending on how many Connections
   the library should create.

- C99 Compiler and Build System

   You will need a C99 compiler installed to build the library. The 
   GNU C compiler (GCC) from the Free Software Foundation (FSF) is
   recommended. In addition, your PATH must contain basic build tools
   such as make and database configuration scripts for MySQL and 
   PostgreSQL, that is, mysql_config and pg_config respectively.
   
- Database systems
 
   This Software supports the following database systems, 
     - MySQL         - version 4.1 or above
     - PostgreSQL    - version 8.0 or above 
     - SQLite        - version 3.0 or above
     - Oracle        - version 10 or above
   Client libraries for at least one of these database systems must
   be installed on the host on which this Software will be built.
 
 
## Installation
 
 This library utilize the GNU auto-tools and provided the requirements
 above are satisfied, building the library is conducted via the
 standard;

```bash
  autoreconf --force --install
  ./configure --without-postgresql
  make
  make install 
```
 
 Use `./configure --help` for build and install options. By default, the
 library is built with support for MySQL, PostgreSQL and SQLite. You may
 change this with the `--without-<database>` options to `./configure`. E.g.
 `--without-mysql, --without-postgresql` or `--without-sqlite`. 
 
 To verify the library and run unit tests, do `make verify`. You may
 also want to take a look at test/select.c for an example on how to use
 the library.
  
 Note that unit tests cannot be built if the `--enable-protected`
 configure switch was used. This switch is used to package protect
 non-API objects in the library. It is strongly recommended to build the
 library with `--enable-protected` as it will be faster and reduce the risk
 for name symbol interposing


## API Documentation
 
 The directory doc/api-docs/ and index.html contains the full API
 documentation for the library, generated by Doxygen. Start by reading
 the documentation for ConnectionPool.h
  

## Exceptions handling
 
 The library implements an elegant solution for thread-safe exceptions
 handling. Use of exceptions frees programmers from the tedious return
 code idiom for dealing with errors. The API documents every method that
 can throw an exception. Methods that can throw an exception should be
 called from inside a try-block.
  

## Link and include
 
 Clients may use the following meta interface to include libzdb API
 interfaces;
 
 ```c
 #include <zdb.h>
 ```
 
 Alternatively, libzdb API interfaces can be included separately
 as needed.

 Compile and link with libzdb;

```c
 gcc -o select select.c -L/<prefix>/lib -lzdb -I/<prefix>/include/zdb
```

 On some systems you may have to explicit link with -lpthread and
 set LD_LIBRARY_PATH if libzdb was installed in a non-standard location
 
 Libzdb can be used directly in a C++ or in a Objective-C(++) project. The 
 `<zdb.h>` header contains the `extern "C"` statement which is required when
 importing C declarations into C++ code and linking with a C library.
 
  
## License Notes

 This Software product is licensed under the GNU General Public License
 version 3. You can use this Software product free of charge to develop,
 use and distribute Open Source application programs, including reusable
 components and other software that link with the Software. You may also
 use and modify any example source code included with the Software for
 any purpose.
  
 See the file COPYING accompanying the Software for details. 


## Reporting a bug

 If you believe you have found a bug, please use the issue tracker 
 mentioned at http://www.tildeslash.com/libzdb/#contact to report the 
 problem. Remember to include the necessary information that will enable 
 us to understand and reproduce this problem. Alternatively, you can
 send us an [email](bugs-libzdb@tildeslash.com)


## Questions and support

 If you have questions or comments about the software or documentation 
 please subscribe to the libzdb general mailing list and post your 
 questions there. 
 
   http://www.tildeslash.com/mailman/listinfo/libzdb-general


## Contributing
 
 You are welcome to contribute to this project, but please note that
 an electronically signed CLA is required to be on file before any Pull 
 Request or patches are accepted or you are given commit rights to the 
 project. To sign, go to http://tildeslash.com/cla/


## Contact information

 Libzdb is a product of Tildeslash Ltd. a company registered in
 Norway and in United Kingdom.
 
 For further information about this Software, please use the following 
 contact information.

 E-mail:
   info@tildeslash.com

 Internet:
   http://www.tildeslash.com/libzdb/
   

## Acknowledgments

 The design of this library was inspired by principles put forth by 
 David R. Hanson <drh@drhanson.net> in his excellent book 
 "C Interfaces and Implementations". You can learn more about this 
 book [here](http://www.cs.princeton.edu/software/cii/)

