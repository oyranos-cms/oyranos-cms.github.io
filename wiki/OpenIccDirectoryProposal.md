---
title: OpenIccDirectoryProposal
permalink: wiki/OpenIccDirectoryProposal/
layout: wiki
tags:
 - Concepts
 - Oyranos
---

| Revision History |
|------------------|
| Revision 0.1     |
||
| Revision 0.1.1   |
||

<H1>
OpenICC Directory Proposal

</H1>
ICC profiles and characterisation data, settings and registration files
need a proper place in the file hierarchy. This proposal describes
common practise and new suggestions.

Each directory contains a substructure to hold different data. The
naming should provide a hint what it contains.

Scope
-----

The proposal is primarily suggested for Unix alike systems, such as the
BSD's and Linux.

Systems like osX and Solaris will probably provide different places or
means to register ICC profiles and settings. A programming interface,
like the path API's in Oyranos, should cover these specific cases.

General OpenICC Paths
---------------------

The Users path should be located in:

***$XDG\_CONFIG\_HOME/color*** or alternatively

***$HOME/.config/color*** for as a top directory to store configuration
files in its subdirectories.

***$XDG\_DATA\_HOME/color*** or alternatively

***$HOME/.local/share/color*** shall be used as a top directory to store
data files in it's subdirectories like ICC profiles.

For the XDG\* variables see \[1\].

$HOME/.color can be considered deprecated and should fade out.

As system wide installation paths exist the XDG\_DATA\_DIRS variable,
which itself can contain several directory entries:

***$XDG\_DATA\_DIRS***\[0\]***/color***,
***$XDG\_DATA\_DIRS***\[1\]***/color*** and so on, or alternatively

two system paths, due to different system directory layouts, exist and
should be searched for:

***/usr/local/share/color***

and

***/usr/share/color*** as typical for Linux packages.

An application path points to:

***$PREFIX/share/color***

These paths are considered top level entry points and should contain
almost no files. Each specific data path, containing the actual data, is
each located below these general OpenICC paths.

Typical colour configuration data is architecture independent. The
configuration can therefore stay in one place as further described
below. Architecture dependent CMM modules and utilities should go into
the usual file system places for libraries and binary executables.

Colour Profile Paths
--------------------

The colour management systems should provide various locations for
storing common place colour profiles. The directory name is

***icc***/

The directory expands then for instance to /usr/share/color/icc. The icc
subdirectory should be scanned recursively, to allow some future
features.

### Subdirectory naming rules

Profiles can grouped by different purposes. Therefor some directory
names are reserved for future expansion. They are mentioned below:

'editing' 'device' 'camera' 'scanner' 'monitor' 'printer' 'output'
'input' 'abstract' 'named\_color\_list' 'colorspace' 'file' 'standard'

The above names are not yet in use. So don't rely on them, just avoid
using. You can activate easily after further discussion at the OpenICC
email list. So a scheme like:

`/usr/share/color/icc`  
`   vendor/`  
`       rgb/`  
`           vendor_rgb.icc`  
`       cmyk/`  
`           vendor_fogra27.icc`  
`           vendor_fogra28.icc`  
`           ...`

would make complete sense.

Settings
--------

Settings may contain presets of single settings. The location is at:

***settings***/

CMMs
----

CMM's register data can be stored in:

***cmms***/

Technical implementation
------------------------

The profile paths exist on system level in the file hierarchy.

References
----------

\[1\] [XDG Environment variables
specification](http://standards.freedesktop.org/freedesktop-platform-specs/1.0/basedir-spec-0.6/ar01s03.html)

\[2\] [freestandards.org bug
\#77](http://bugs.freestandards.org/show_bug.cgi?id=77)

Acknowledgments
---------------

The presented concepts where discussed on the OpenICC email list at
fd.o, or reached this document by a bug entry comment \[2\].
