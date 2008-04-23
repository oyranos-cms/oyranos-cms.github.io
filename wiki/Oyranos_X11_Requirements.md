---
title: Oyranos/X11 Requirements
permalink: wiki/Oyranos/X11_Requirements/
layout: wiki
tags:
 - Oyranos
 - Standards
---

Oyranos has some requirements to provide colour management related
informations through it's APIs. For further reading see [Monitor
Configuration](/wiki/Monitor_Configuration "wikilink").

Architectural Overview
----------------------

Applications need a way to communicate colorimetry of their image
content. Applications, which like to handle colour management (CM) on
their own, need additional a path to tell the system what to do with the
content and what not.

Applications can follow several strategies:

1.  be dumb - The application knows nothing about CM. The system takes
    content as being in a default RGB colour space and does colour
    matching. Most applications would fall in this category.
2.  tag content - The application knows about the colorimetry of its
    content and tells the system about it.
3.  take over control - The application knows best how to handle its
    content. Tell the system to not match content with following
    options:
    1.  Dont apply colour conversions. This is for proofing and image
        editing applications.
    2.  Dont apply calibration from graphic card gamma tables. This is
        useful for HDR content.

The “take over control” kind of applications want additionally to know
about the screen layout and monitor colorimetry. This is handled by
Xinerama alike API's and the
[\_ICC\_PROFILE\_xxx](#ICC_Profiles_in_X "wikilink") atom.

### Screen Areas and Colour Space tagging

Two things are needed,

-   a ICC profile container attached to window or screen region
-   a opt out flags for colour correction down the path, so applications
    can handle colour management on their own
    -   a “no colour conversions” flag
    -   a “no calibration from graphic card gamma tables” flag
-   the virtually thierd is that every other content is expected as
    sRGB, as is the case today

The above would fit along all the path:

` application -> toolkit -> composite manager -> X11 -> OpenGL -> shader.`

There remains to find an endpoint where most paths meet. This could be
the composite manager or a additional layer between composite manager
and Xorg.

Multi Monitor EDID in X11
-------------------------

EDID information describes monitor parameters like description, serial
number and gives hints about colourimetric behaviour.

Oyranos uses this information to identify a particular monitor and
search for a best matching profile, as long as one is stored in the
Oyranos device profile database.

### Specification

X servers export the EDID inormation typically in the
“XFree86\_DDC\_EDID1\_RAWDATA” and “XFree86\_DDC\_EDID2\_RAWDATA” atom.
If there are more monitors connected to the root window, the following
atoms get a underscore and the monitor number appended, like in

### Example

Xinerama\_screen\_number = 0 =&gt; XFree86\_DDC\_EDID1\_RAWDATA

Xinerama\_screen\_number &gt;= 1 =&gt; XFree86\_DDC\_EDID1\_RAWDATA\_1 +
XFree86\_DDC\_EDID1\_RAWDATA\_2 ...

This way compatibility is enshured for existing applications.

### Parsing

The section decribes the EDID 1 parsing in Oyranos.

Oyranos parses EDID 1 information for monitor identification. It uses
the 18 byte blocks starting from 54 for a monitor manufacturer, model
and serial ID string. In case the manufacturer was omitted, it switches
back to scan the 2 byte ID's starting at position 8. The later could be
extended to model(10) and serial(12).

### References

-   The issue was initially thrown to [the fd.o
    bugtracker](https://bugs.freedesktop.org/show_bug.cgi?id=3910).
-   [Re: DDC Atoms &
    Xinerama](http://www.mail-archive.com/devel@xfree86.org/msg01297.html)

### Versions / Implementations

Oyranos 0.1.5 obtained the oyranos-monitor-nvidia commandline tool to
demonstrate the described behaviour.

ICC Profiles in X
-----------------

### References

-   [\#Multi Monitor EDID in X11](#Multi_Monitor_EDID_in_X11 "wikilink")
-   [ICC Profiles in X Specification
    0.2](/wiki/ICC_Profiles_in_X_Specification_0.2 "wikilink")

### Further Tasks

[(Draft for a ICC Profiles in X Specification
0.3)](/wiki/ICC_Profiles_in_X_Specification_0.3 "wikilink")

-   (done) possibly add a \_ICC\_IN\_X\_VERSION atom can be included to
    talk about the revision supported by the system
    [1](http://lists.freedesktop.org/archives/openicc/2007q4/000987.html)
-   (done) clarify about current(v0.2) ambiguities regarding monitor and
    screen counting starting from zero
-   (done) clarify about current(v0.2) ambiguities regarding screens and
    pseudo - or Xinerama screens
-   (done) Jon A. Cruz suggested to use monitor as a basic term instead
    of screen
    [2](http://lists.freedesktop.org/archives/openicc/2007q4/001056.html)
-   (done) Hal: substitute *uncalibrated* with *uncharacterized* to show
    that the vcgt issue is not targeted
    [3](http://lists.freedesktop.org/archives/openicc/2007q4/000989.html)
-   (done) set default for uncharacterised to sRGB
    [4](http://lists.freedesktop.org/archives/openicc/2005q2/000431.html)
-   neutral hosting at fd.o see [bug
    \#12824](https://bugs.freedesktop.org/show_bug.cgi?id=12824)
-   (done) correct case of ICC\_PROFILE\_xxx
    [5](http://lists.freedesktop.org/archives/openicc/2008q2/001579.html)

As soon as the discussion on the [OpenICC](/wiki/OpenICC "wikilink") list
settles, revision 0.3 will be drafted and can be finally released after
a small period.

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
