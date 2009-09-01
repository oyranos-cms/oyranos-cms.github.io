---
title: Oyranos/Debugging
permalink: wiki/Oyranos/Debugging/
layout: wiki
---

Debugging hints for Oyranos.

### Enable Debugging

**Build Oyranos** with debugging informations by using the *configure*
option *--enable-debug*.

### Debug Messages

Setting the *OYRANOS\_DEBUG* variable to a integer higher than zero e.g.
“OYRANOS\_DEBUG=2” gives some debug output.

### Backtrace

To obtain a back trace use
OYRANOS\_BACKTRACE=oyranos\_message\_sequence. Note the
oyranos\_message\_sequence must be visible for the back trace to apply,
e.g. OYRANOS\_BACKTRACE=oyranos\_cmm\_oyX1.c my\_app should back trace
the calls into the oyX1 module.

### Recommended Tools

**Memory debuggers** like [valgrind](http://www.valgrind.org) are very
helpful tools. It is a fine tool to spot errors in C and C++ code early.

**Traditional debuggers** like *gdb* or the *VC++* internal one are very
basic and helpful tools. In case of a crash it is often very simple to
just run the program under the debugger and then examine the function
stack and look around what happened in the surrounding of the crash. It
might be easy to spot that place as well with a memory debugger. But a
general debugger allows to step around and to better understand the
code. To place a breakpoint before the crash section might be a good
idea to see what lead to the buggy situation.

### Common Debug Scenarios

**Display of local variables** together with the **function arguments**
inside a general debugger is IMO very useful. This data is already
visible in XCode and VC++. In *DDD* it can be enabled as follows. First
enable the data view: *\[topmenu\[View\]\]-&gt;Data Window ...* Then in
the data view display the desired variables:
*\[topmenu\[Data\]\]-&gt;Display Arguments* and
*\[topmenu\[Data\]\]-&gt;Display Local Variables*.

**Modules** are somewhat tricky to step through, as its harder to set
breakpoints before the dynamic modules are loaded. One way is to set a
endless loop, e.g. “while(1) dummy=dummy+1;”, at the desired point in
the modules sources and recompile and install. *make install\_bin* is a
abbreviation. The program should run into the set loop if calling the
according function in that module. Its then easy to stop that loop and
move the execution pointer outside the loop to start stepping through
the code.

### References

GDB and DDD come with most Linux distributions and expectedly can be
easily installed on BSD. DDD is a front end for gdb.

XCode is included in Apples development tools.

VC++ can be obtained from Microsoft. Since 2005 exists a free of charge
version for C and C++ development.

Back =&gt; [Oyranos\#Development](/wiki/Oyranos#Development "wikilink")
