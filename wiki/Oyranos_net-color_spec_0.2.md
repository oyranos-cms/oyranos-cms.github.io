---
title: Oyranos/net-color spec 0.2
permalink: wiki/Oyranos/net-color_spec_0.2/
layout: wiki
---

<h1>
DRAFT

</h1>
| Revision History                                                                                                                                                                    |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Revision 0.0](http://www.oyranos.org/scm?p=xcolor.git;a=blob;f=docs/net-color-spec;h=c3a5776124cf16d9636cf1a65bc130082b531049;hb=1cf1107d8679161e990c3cf67371f0acb630686e)         |
| [Revision 0.2 DRAFT 1](http://www.oyranos.org/scm?p=xcolor.git;a=blob;f=docs/net-color-spec;h=94a8349f81670f23088959a6e4b524af8a8f11b7;hb=ab8775f7e8777de5da3be04cc92bc6a883432261) |
||

Introduction
------------

The net-color spec defines a protocol which can be used by X11 clients
to offload color correction and transformation into the compositing
manager. The basic idea is to communicate client side regions to the X11
server. The regions can of this version have no ICC profile attached,
which means a color server, typical in a compositing manager, shall not
color manage these regions. These regions then are in the responsibility
of the application.

Color Region
------------

A color region is described by the following C structure:

`typedef struct {`  
`  uint32_t region;  /* window centric XserverRegion               */`  
`  uint8_t md5[16];  /* ICC MD5 hash of the associated ICC profile */`  
`} XcolorRegion;`

It defines a region and the attached color profile. Color regions are
attached to windows and used by the compositing manager to apply the
proper color transformation. Windows can have an unlimited amount of
regions attached, though only the first 2 \* 2^32 can be referenced. As
of this spec the md5 shall be set to zero to signal the region is
already color managed by the application.

Atoms
-----

### \_NET\_COLOR\_REGIONS

The atom is attached to windows and lists the XcolorRegion's defined for
that specific window. The application is responsible to update the
contained informations, e.g. on region resize or move inside the window.
The type is XA\_CARDINAL and values are stored in network byte order.

### \_NET\_COLOR\_TARGET

Is attached to windows and specifies on which output the window should
look correctly. The type is XA\_STRING.

### \_NET\_COLOR\_DESKTOP

The atom is attached on the root window to tell about a color servers
activity. The content is of type XA\_STRING and has four sections
separated by a empty space char ' '. The \_NET\_COLOR\_DESKTOP atom is a
string with following usages: - uniquely identify the colour server -
tell the name of the colour server - tell the colour server is alive All
sections are separated by one space char ' ' for easy parsing.

The first section contains the process id (pid\_t) of the color server
process, which has set the atom. The second section contains time since
epoch GMT as returned by time(NULL). The thired section contains the bar
'|' separated and surrounded capabilities: - NCP \_NET\_COLOR\_PROFILES
- NCT \_NET\_COLOR\_TARGET - NCM \_NET\_COLOR\_MANAGEMENT - NCR
\_NET\_COLOR\_REGIONS - V0.3 indicates version compliance to the
\_ICC\_Profile in X spec The fourth section contains the server name
identifier.

As of this specification the third section must contain NCR and the
supported \_ICC\_PROFILE in X version. NCT is optional.

A example of a valid atom might look like: \_NET\_COLOR\_DESKTOP(STRING)
= “4518 1274001512 |NCR|V0.3| compiz\_colour\_desktop”

References
----------

-   X window system (http://www.x.org)
-   International Color Consortium (http://www.color.org)
-   \_ICC\_Profile in X
    (http://www.freedesktop.org/wiki/Specifications/icc\_profiles\_in\_x\_spec)
-   Xcolor reference implementation (git clone
    <git://www.oyranos.org/git/xcolor>)
-   colour\_deskop colour server for compiz (git clone
    <git://www.oyranos.org/git/oyranos>)
-   xcmsevents monitor tool (git clone
    <git://www.oyranos.org/git/oyranos>)

Todo
----

The relation to the \_ICC\_Profile in X spec is undefined in that a
monitor profile as provided by the \_ICC\_PROFILE(\_xxx) atom is for
unaware applications not correct during the run of the color server.
Necessarily a double color conversion will happen for net-color spec
unaware applications, which is a clear conflict. A
\_ICC\_DEVICE\_PROFILE(\_xxx) atom during color server run is in
discussion.

2008 (c) Tomas Carnecky, 2010 (c) Kai-Uwe Behrmann
