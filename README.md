
## Introduction

This is a fork of the pymotion library, that version is broken on OSX 10.6. I'm trying to
get it working again.

### Links
* [Unimotion](http://unimotion.sourceforge.net/)
* [Patch for Unimotion](http://sourceforge.net/tracker/index.php?func=detail&aid=2943535&group_id=169958&atid=852436)

### Status and notes

I was able to patch unimotion.c - the copy here is the same as the original. Build arguments seem wrong, though.

Unimotion is written to become a dynamic library only. I was able to get it to build the required x86_64 arch by changing unimotion/Makefile:
<pre>
CFLAGS=-Wall -Os -g -isysroot /Developer/SDKs/$(SDK) -arch i386 -arch ppc -arch x86_64 -fconstant-cfstrings
LFLAGS=-Wl,-syslibroot,/Developer/SDKs/$(SDK) -arch i386 -arch ppc -arch x86_64 -framework IOKit -framework CoreFoundation
</pre>
But then the libUniMotion.dylib has to be in the Python binary directory, and still fails. Drat.

Tried creating unimotion.so, but that doesn't work either, I lack knowledge of the Framework/shared object boundary and interactions.

*I'm currently stumped.* Help is welcome.