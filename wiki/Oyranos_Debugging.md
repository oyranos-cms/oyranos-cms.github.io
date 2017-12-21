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

Setting the *OY\_DEBUG* variable to a integer higher than zero e.g.
“OY\_DEBUG=2” gives some debug output.

-   see as well [Oyranos Environment
    Variables](http://www.oyranos.org/doc/environment.html)

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

**Modules** are sometimes tricky to step through, as it can be harder to
set breakpoints before the dynamic modules are loaded. It might be
easier to run the application and kill it after passing the code path of
interesst. The open the sources from *\[topmenue\[File\]\]-&gt;Open
Sources...* and set the breakpoint in the opened source file and
restart. If the normal way of setting breakpoints does not succeed the
following might help. One way is to set a endless loop, e.g. “while(1)
dummy=dummy+1;”, at the desired point in the modules sources and
recompile and install. The program should run into the set loop if
calling the according function in that module. Its then easy to stop
that loop and move the execution pointer outside the loop to start
stepping through the code.

**Tracking lost objects** is possible with the OY\_DEBUG\_OBJECTS
environment variable and its population to the oy\_debug\_variable. If
the program has placed a oyObjectTreePrint() the object graph will be
shown as a SVG graphic at the time of calling this function. It is good
to call oyObjectTreePrint() after releasing all used objects. Then only
caches should be visible and not properly dereferenced objects.
OY\_DEBUG\_OBJECTS works pretty fine grained, while oyObjectTreePrint()
will show all known not deallocated objects.

### References

GDB and DDD come with most Linux distributions and expectedly can be
easily installed on BSD. DDD is a front end for gdb.

XCode is included in Apples development tools.

VC++ can be obtained from Microsoft. Since 2005 exists a free of charge
version for C and C++ development.

Back =&gt; [Oyranos\#Development](/wiki/Oyranos#Development "wikilink")
