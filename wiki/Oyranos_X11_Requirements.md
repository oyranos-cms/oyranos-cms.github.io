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
-   the virtually third is that every other content is expected as sRGB,
    as is the case today

The above would fit along all the path:

` application -> toolkit -> composite manager -> X11 -> OpenGL -> shader.`

There remains to find an endpoint where most paths meet. This could be
the composite manager or a additional layer between composite manager
and Xorg or inside Xorg itself.

The OpenICC project [Colour Management Near
X](http://www.freedesktop.org/wiki/OpenIcc/ColorManagementNearX)
implemented the idea. As a result the X Color Management spec was born
to describe the basic communication. It covers and continues most of the
above outlined ideas.

Multi Monitor EDID in X11
-------------------------

EDID information describes monitor parameters like description, serial
number and gives hints about colourimetric behaviour.

Oyranos uses this information to identify a particular monitor and
search for a best matching profile, as long as one is stored in the
Oyranos device profile database.

You can check independently whether a EDID atom is set by calling in a
X11 environment:

`xprop -root | grep EDID`

The modern way is to search for the EDID data in the xrandr output:

`xrandr --prop | grep EDID`

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

This section is incomplete. But at least the code can be found here in
libXcm-0.3.x and higher.

The section decribes the EDID parsing in Oyranos.

Oyranos parses EDID information for monitor identification. It uses the
18 byte blocks starting from 54 for a monitor manufacturer, model and
serial ID string. In case the manufacturer was omitted, it switches back
to scan the 2 byte ID's starting at position 8. The later could be
extended to model(10) and serial(12).

### References

-   The issue was initially thrown to [the fd.o
    bugtracker](https://bugs.freedesktop.org/show_bug.cgi?id=3910).
-   [Re: DDC Atoms &
    Xinerama](http://www.mail-archive.com/devel@xfree86.org/msg01297.html)
-   [support request for XRandR in nv and nvidia
    drivers](https://bugs.freedesktop.org/show_bug.cgi?id=16639)

### Versions / Implementations

Oyranos 0.1.5 obtained the oyranos-monitor-nvidia commandline tool to
demonstrate the described behaviour.

ICC Profiles in X
-----------------

### References

-   [\#Multi Monitor EDID in X11](#Multi_Monitor_EDID_in_X11 "wikilink")
-   [ICC Profile in X
    Specification](http://www.freedesktop.org/wiki/Specifications/icc_profiles_in_x_spec)
    @ fd.o
-   older versions can be found in the
    [Category:Standards](http://www.oyranos.org/wiki/index.php?title=Category:Standards)

### Further Tasks

[(Draft for a ICC Profiles in X Specification
0.5)](/wiki/ICC_Profiles_in_X_Specification_0.5 "wikilink")

-   add xrandr-1.2 porperties per each physical output device

net-color spec
--------------

The goal is to communicate ICC colour regions between a colour server
and clients.

### References

[Draft of net-color spec 0.2](/wiki/Oyranos/net-color_spec_0.2 "wikilink")

### Implementations

The implementation is available in
[libXcm-0.2.x](http://www.spinics.net/lists/xorg/msg50027.html) and
later.

The CompIcc ICC colour server for compiz plugin supports the draft. The
plugin supports complete desktop colour correction and is multi monitor
aware.

Ideas exist to support the spec in a Gnome window manager.

### Further Tasks

-   screenshot tools
    -   take tagged regions as is - they are already colour corrected
    -   convert remaining desktop from native monitor space to document
        colour space
    -   use document colour space from \_ICC\_PROFILE(\_xxx) (typical
        sRGB)
-   describe \_NET\_COLOR\_PROFILES (3D scene/2D vector colour
    correction)
    -   server and client side implementation

Miscellaneous
-------------

### References

30-bit visual bugs

-   [Graphical corruption in the splash screen when using a depth 30
    desktop](https://bugs.kde.org/show_bug.cgi?id=214011)
-   [30-bit drawables remain
    black](https://bugzilla.gnome.org/show_bug.cgi?id=625202) (in Gtk)

Colour Management and Toolkits

-   ICC colour management policiy
    -   [FLTK feature request](http://www.fltk.org/str.php?L2411)
    -   [Qt feature
        request](http://bugreports.qt.nokia.com/browse/QTBUG-6582)

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
