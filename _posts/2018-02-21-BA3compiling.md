---
layout: post
title:  "Cross-compiling BayesAss for OS X"
date:   2018-02-21 14:29:42 -0700
categories: jekyll update
---


# Why cross-compile?
The [Mac OS X](https://en.wikipedia.org/wiki/MacOS) operating system has changed over the years both in terms of advancing (and backward-incompatible) OS X releases (32-bit versus 64-bit, etc.) running on a common chip architecture (Intel) and in terms of chip architectures (PowerPC versus Intel). Here I focus on compiling compatible binaries for use on Intel chips running either 32-bit or 64-bit releases of OS X that are not backward compatible (i.e., binaries compiled for a more recent OS X release will not execute on an older release). Along the way I will talk about compiling portable (in Mac lingo universal) binaries that run on multiple versions of OS X, as well as ways to include external libraries when distributing command line programs for OS X.

The procedures outlined here are specific to command line programs written in the C/C++ languages.  The focus will be on what I needed to do to produce binaries of my own software BA3 (which uses the [gsl](https://www.gnu.org/software/gsl/) library) for use on different Mac OS X versions.  The procedures are pretty generic, however, so this should hopefully be a useful guide for others planning to distribute a compiled C/C++ command line program for OS X. Apple began the transition to Intel processors in 2005. OS X 10.5 Leopard supported both PowerPC and Intel processors (32-bit and 64-bit).  Support for PowerPC was offically dropped in 2009 with the release of Mac OS X 10.6 Snow Leopard which supported either 32-bit or 64-bit mode. OS X 10.7 and later versions only support 64-bit mode. So, in practical terms if a binary is to run on all possible Intel-based Macs it should be compiled to run on OS X 10.5 and later releases. That will be the objective here.

# Getting ready to compile
I will use the standard Mac development environment [X Code](https://developer.apple.com/xcode/) (currently Xcode 9) in this tutorial but limited experimentation suggests it also works with a modern GCC installation (installed with [Homebrew](https://brew.sh/) for example).  To follow along install the latest version of OS X which is available free through the Mac app center. XCode was originally built around the GCC compiler utilities but switched exclusively to Clang+LLVM in 2011 (Xcode 4.2). The gcc command still exists but is purely for handling legacy code. Opening the Terminal application after installing XCode and typing `gcc -v` will confirm that the command is a virtual link to the clang compiler. No worries though as most code that compiles with gcc on other platforms (e.g., Linux) will compile just fine with clang. Create a file named darwin.cpp for testing purposes that has the following content:
```cpp
#include<iostream>
namespace std;
int main()
{
	cout << "\"An American monkey, after getting drunk\n";
	cout << "on brandy, would never touch it again and\n";
	cout << "thus was wiser than many men.\"\n";
	cout << "Charles Darwin.\n";
	return 0;
}
```
First, compile this code using no command line options:
```
c++ darwin.cpp -o darwin64
```
To see the details of the binary file produced you can use the unix command `file` as follows:                               
```
bruce$ file darwin64
darwin64: Mach-O 64-bit executable x86_64
```
The result is a 64-bit binary that will run on a modern 64-bit OS X release only.
Now instead compile the C++ code using the following command:
```
c++ -arch i386 -mmacosx-version-min=10.5 darwin.cpp -o darwin32
```
This will create a binary file that is capable of being run on a 32-bit OS X operating system as old as OS X 10.5. To see the details you can again use the unix command `file`:
```
bruce$ file darwin32
darwin32: Mach-O executable i386
```
To test that the file is indeed compatible with an older OS X release you need a surplus Mac (running OS X 10.6 or earlier in 32-bit mode). For testing purposes I
keep an old Mac mini on hand that is running OS X 10.6 (without 64-bit extensions).  

# Creating a universal binary
At this point we have two binaries darwin32 and darwin64 to distribute to users with different OS X versions (pre-OS X 10.7 and post-OS X 10.7, respectively). It would obviously be more convenient (and less confusing for users) if we could instead distribute a single binary for all targetted platforms. A single binary that includes machine code for multiple architectures is called a universal (or "fat") binary in the Mac lingo. We will use the program `lipo` to create a universal binary from the two binaries we have compiled. First, we use `lipo` to examine each binary and confirm that it specifies a single architecture:
```
bruce$ lipo -info darwin64
Non-fat file: darwin64 is architecture: x86_64

bruce$ lipo -info darwin32
Non-fat file: darwin32 is architecture: i386

```
Next we use `lipo` to combine the two binaries into one universal binary:
```
lipo -create darwin32 darwin64 -o darwin
```
and now checking the binary gives:
```
bruce$ lipo -info darwin
Architectures in the fat file: darwin are: i386 x86_64
```

# Including an external library
Thus far we have learned how to compile a simple stand-alone source file into a universal binary. Now I turn to the more difficult
task of compiling a universal binary of the BA3 program. In this case, there is the additional complication that BA3 relies on
an external math library, the [Gnu Scientific Library](https://www.gnu.org/software/gsl/) (or gsl). There are
two issues associated with this: first, newer versions of OS X strongly discourage static linking of libraries
pretty much forcing a dynamic library to be distributed along with the program binary which is a nuisance and
potential source of errors for users (who might fail to include the library in the appropriate subdirectory when
moving the program around). Second, two versions of the library need to be compiled: one for the early-OS 32-bit binary
and one for the 64-bit binary. Failing to do this will lead to a linker error. First, download the latest version of gsl.
Then, to compile the 32-bit library in the gsl root directory type:
```
 ./configure CC="gcc -arch i386 -mmacosx-version-min=10.5" CXX="g++ -arch i386 -mmacosx-version-min=10.5" CPP="gcc -E" CXXCPP="g++ -E"
```
Then type `make` and after the compilation finishes type `cp -Rf .libs libsi386` to copy the libraries to a labelled folder for later use.
Use `file` to check the architecture of the dynamic library:
```
bruce$ cd libsi386
Bruces-MacBook-Pro-2:libsi386 bruce$ ls
gsl-histogram	libgsl.19.dylib	libgsl.dylib	libgsl.lai
gsl-randist	libgsl.a	libgsl.la	version.o
Bruces-MacBook-Pro-2:libsi386 bruce$ file libgsl.19.dylib
libgsl.19.dylib: Mach-O dynamically linked shared library i386
```
Then compile the 64-bit library:
```
make clean
./configure
make
```
and again copy the libraries to a new folder `cp -Rf .libs libsX86_64` and check the architecture:
```
bruce$ cd libsX86_64
bruce$ file libgsl.19.dylib
libgsl.19.dylib: Mach-O 64-bit dynamically linked shared library x86_64
```
Now we are ready to compile BA3. Get the [BA3 source code](https://github.com/brannala/BA3) from github. A
makefile with the following contents is used to first compile the 32-bit version:
```
P = BA3
INCLUDE = -Iinclude -I/Users/bruce/gsl-2.2.1/gsl-2.2.1/
LIBS = -L/Users/bruce/gsl-2.2.1/gsl-2.2.1/libsi386 
CFLAGS = -Wall -O3 -arch i386 -mmacosx-version-min=10.5
LDLIBS = -lgsl -lcblas
CC=g++
all:
        $(CC) $(CFLAGS) src/main.cpp $(INCLUDE) $(LIBS) $(LDLIBS) -o BA3i386
```
You will need to alter the paths for -L and -I to point to your local directory containing the gsl libraries and headers. Make
the binary and then check the architecture:
```
bruce$ file BA3i386
BA3i386: Mach-O executable i386
```
Now create a revised makefile for compiling the 64-bit binary:
```
P = BA3
INCLUDE = -Iinclude -I/Users/bruce/gsl-2.2.1/gsl-2.2.1/
LIBS = -L/Users/bruce/gsl-2.2.1/gsl-2.2.1/libsX86_64 
CFLAGS = -Wall -O3
LDLIBS = -lgsl -lcblas
CC=g++
all:
        $(CC) $(CFLAGS) src/main.cpp $(INCLUDE) $(LIBS) $(LDLIBS) -o BA3X86_64
```
Make the binary and again check the architecture:
```
bruce$ file BA3X86_64 
BA3X86_64: Mach-O 64-bit executable x86_64
 ```                                                                                                  
Okay, so far so good. Now we need to move the binaries and libraries to a common directory that can be compressed and distributed to
BA3 users.
```
bruce$ mkdir ~/BA3
bruce$ cp ~/github/BA3/BA3i386 ~/BA3 
bruce$ cp ~/github/BA3/BA3X86_64 ~/BA3 
bruce$ mkdir ~/BA3/lib32
bruce$ mkdir ~/BA3/lib64
bruce$ cp /Users/bruce/gsl-2.2.1/gsl-2.2.1/libsX86_64/libgsl.19.dylib ~/BA3/lib64
bruce$ cp /Users/bruce/gsl-2.2.1/gsl-2.2.1/libsi386/libgsl.19.dylib ~/BA3/lib32
bruce$ cd ~/BA3 
```
For each of the binaries we need to specify the new path to the shared library. This is done using the unix `otool` program. First, we examine the current path for 32-bit library:
```
bruce$ otool -D ~/BA3/lib32/libgsl.19.dylib
/Users/bruce/BA3/lib32/libgsl.19.dylib:
/usr/local/lib/libgsl.19.dylib
```