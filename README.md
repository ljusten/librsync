# README for librsync

librsync implements the rolling-checksum algorithm of remote file
synchronization that was popularized by the rsync utility and is used in
rproxy. This algorithm transfers the differences between 2 files without
needing both files on the same system.

librsync's canonical branches (since 2014-04) are at

  https://github.com/librsync/librsync/

## Requirements

To build librsync you will need:

* A C compiler and appropriate headers and libraries

* Make

* popt -- command line parsing library

  Available from http://rpm5.org/files/popt/

## Compiling

To build and test librsync from the extracted distribution do;

   $ ./configure
   $ make all check

## Note for RedHat 7.0

RedHat 7.0 (Guiness) ships with a buggy version of GCC 2.96 that
produces many warnings while compiling librsync.  These are harmless
-- the library seems to work anyhow.  You can avoid the warnings by
using the 'kgcc' version of the compiler:

   $ export CC=kgcc
   $ ./autogen.sh
   $ make all check

## Note for Windows

With cygwin you can build using gcc as under a normal unix system. It
is also possible to compile under cygwin using MSVC++. You must have
environment variables needed by MSCV set using the Vcvars32.bat
script. With these variables set, you just do;
  
   $ ./configure.msc
   $ make all check

The PCbuild directory contains a project and pre-generated config
files for use with the MSVC++ IDE. This should be enought to compile
rdiff.exe without requiring cygwin.

## Library Versions

librsync uses the GNU libtool library versioning system, so the filename
does not correspond to the librsync release.  To show the library release
and version, use the librsyncinfo tool. See libversions.txt for more
information.

## Platforms

librsync is known to run on:

GNU Linux Debian 3.0 x86

SUNWspro: (use -v for more warnings)

mips-sgi-irix6.5: works, but you must use GNU Make rather than the default
SGI Make.  I used gcc.

windows32: see above.

## rdiff man page

## Documentation

Documentation for the rdiff command-line tool:

- http://librsync.sourcefrog.net/doc/rdiff.html
- http://librsync.sourcefrog.net/doc/rdiff.pdf

and for the library:

- http://librsync.sourcefrog.net/doc/librsync.html
- http://librsync.sourcefrog.net/doc/librsync.pdf

Generated API documentation:

- https://rproxy.samba.org/doxygen/librsync/refman.pdf
- https://rproxy.samba.org/doxygen/librsync/

## Debugging

If you are using GNU libc, you might like to use

   MALLOC_CHECK_=2 ./rdiff

to detect some allocation bugs. Report any bugs you find to the bug tracker.

## Releasing

Make sure you have cvs2cl installed to generate ChangeLog. Before a
formal release, make sure that the following files have been updated
to reflect the new version:

* AUTHORS - make sure all significant authors are included. 
  
* NEWS - make sure the top "Changes in X.Y.Z" is correct. 
  
* THANKS - make sure the bottom "Contributors for X.Y.Z" is correct.
  
* configure.ac - make sure AC_INIT and librsync_libversion are right.
  
* libversions.txt - make sure libversion is added.
  
* librsync.spec - make sure version and URL are right.
  
* PCBuild/config.h,librsync-config.h - update using configure.msc
  using cygwin.

Do a complete configure and distcheck to ensure everything is properly
configured, built, and tested:

   $ ./autogen.sh [OPTIONS]
   $ ./configure
   $ make distcheck