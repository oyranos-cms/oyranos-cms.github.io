---
title: Oyranos/X11 Requirements
permalink: wiki/Oyranos/X11_Requirements/
layout: wiki
tags:
 - Oyranos
 - Standards
---

Oyranos has some requirements to provide colour management related
informations through it's API.

Multi Monitor EDID in X11
-------------------------

This section is obsoleted since 2006-05-03 by the [ICC Profiles in X
Specification 0.2](/wiki/ICC_Profiles_in_X_Specification_0.2 "wikilink").

EDID information describes monitor parameters like description, serial
number and gives hints about colourimetric behaviour.

Oyranos uses this information to identify a particular monitor and
search for a best matching profile, as long as one is stored in the
Oyranos device profile database.

### Specification

See [ICC Profiles in X Specification
0.2](/wiki/ICC_Profiles_in_X_Specification_0.2 "wikilink").

X servers export the EDID inormation typically in the
“XFree86\_DDC\_EDID1\_RAWDATA” and “XFree86\_DDC\_EDID2\_RAWDATA” atom.
If there are more monitors connected to the root window, the following
atoms get a underscore and the Xinerama screen number appended, like in

### Example

Xinerama\_screen\_number = 0 =&gt; XFree86\_DDC\_EDID1\_RAWDATA

Xinerama\_screen\_number &gt;= 1 =&gt; XFree86\_DDC\_EDID1\_RAWDATA\_1 +
XFree86\_DDC\_EDID1\_RAWDATA\_2 ...

This way compatibility is enshured for existing applications.

### References

-   The issue was initially thrown to [the fd.o
    bugtracker](https://bugs.freedesktop.org/show_bug.cgi?id=3910).
-   [Re: DDC Atoms &
    Xinerama](http://www.mail-archive.com/devel@xfree86.org/msg01297.html)

### Versions / Implementations

Oyranos 0.1.5 obtained the oyranos-monitor-nvidia commandline tool to
demonstrate the described behaviour.

### Further Tasks

(for a v0.3)

-   possibly add a \_ICC\_IN\_X\_VERSION atom can be included to talk
    about the revision supported by the system
-   clarify about current(v0.2) ambiguities regarding monitor and screen
    counting starting from zero
-   clarify about current(v0.2) ambiguities regarding screens and
    pseudo - or Xinerama screens
-   Hal: substitute *uncalibrated* with *uncharacterized* to show that
    the vcgt issue is not targeted

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
