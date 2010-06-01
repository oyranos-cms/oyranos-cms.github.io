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
| Revision 0.1.2   |
| Revision 0.1.3   |
| Revision 0.1.4   |
| Revision 0.1.5   |
| Revision 0.1.6   |
| Revision 0.1.7   |
| Revision 0.1.8   |
| Revision 0.2     |
||

<H1>
OpenICC Directory Proposal

</H1>
ICC profiles and characterisation data, settings and registration files
need a proper place in the directory hierarchy. This proposal describes
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

A top Users colour path should be located in:

***$XDG\_CONFIG\_HOME/color*** and

***$HOME/.config/color*** for a top directory to store human readable
configuration files in its subdirectories.

***$XDG\_DATA\_HOME/color*** and

***$HOME/.local/share/color*** shall be used as a top directory to store
data files in it's subdirectories like ICC profiles.

For the XDG\* variables see \[1\].

$HOME/.color can be considered deprecated and should fade out.

As system wide installation paths exist the ***XDG\_DATA\_DIRS*** and
***XDG\_CONFIG\_DIRS*** variables, which itself can contain several
directory entries:

***$XDG\_DATA\_DIRS***\[0\]***/color***,
***$XDG\_DATA\_DIRS***\[1\]***/color*** and so on, plus

three system paths, due to different system directory layouts, exist and
should always be searched for:

***/usr/local/share/color***

,

***/usr/share/color***

and

***/val/lib/color*** as typical for Linux packages.

These above paths are considered top level entry points and should
contain almost no files. Each specific data path, containing the actual
data, is each located below these general OpenICC paths.

Typical colour configuration data is architecture independent. The
configuration can therefore stay in one place as further described
below. Architecture dependent CMM modules and utilities should reside
below the usual system paths for libraries and binary executables. They
are here not described in detail.

Colour Profile Paths
--------------------

The colour management systems should provide various locations for
storing common place colour profiles. The directory name is

***icc***/

The directory expands then for the /usr/share/color case to
/usr/share/color/icc. Put then the ICC profiles into this or below
/usr/share/color/icc. /usr/share/color should contain only directories
and no ICC profiles. The icc subdirectory should be scanned recursively,
to allow some future features.

So far, installing in a flat hierarchy is ok.

Profiles may be grouped by different purposes. Therefor some directory
names are reserved for future expansion. Candidates are mentioned below:

'editing' 'device' 'camera' 'scanner' 'monitor' 'printer' 'output'
'input' 'abstract' 'named\_color\_list' 'colorspace' 'file' 'standard'

The above names are not yet in use. Don not rely on them, just avoid
using. They can be activated easily after further discussion at the
OpenICC email list.

Settings
--------

Settings may contain presets of single settings. The location is at:

***settings***/

Binary blobs should be preferedly go the \_DATA\_ and clear text ones
the \_CONFIG\_ route.

Installation
------------

It is recommended to ask for the XDG variables befor installing globaly
visible data on a system.

In contrary to create packages with static file locations, like RPM, use
the provided static paths only.

For ICC profiles this would be:

  
*/usr/local/share/color/icc*

*/usr/share/color/icc*

*/var/lib/color/icc*

*~/.local/share/icc*

Technical implementation
------------------------

The profile paths exist on system level in the file hierarchy.

For the XDG variables see \[1\].

### Linking

Linking is allowed, as long as the system supports this, only inside the
a OpenICC top entry path. So it is allowed to set a link from a special
profile file name to a more general one.

` XYZ.icc => VENDOR/Vendor_XYZ.icc`

It's not required and not recommended that a file outside a single top
OpenICC path can be reached.

` !XYZ.icc => /etc/XYZ.icc! or`  
` !/usr/local/share/color/icc/XYZ.icc => ../../../../share/color/icc/XYZ.icc!`

Acknowledgments
---------------

The presented concepts where discussed on the OpenICC email list at
fd.o, or reached this document by a bug entry comment \[2\].

References
----------

\[1\] [XDG Environment variables
specification](http://standards.freedesktop.org/freedesktop-platform-specs/1.0/basedir-spec-0.6/ar01s03.html)

\[2\] [freestandards.org bug
\#77](http://bugs.freestandards.org/show_bug.cgi?id=77)

Discussion
----------

The /var/lib/color path is required to store system wide local machine
data by a administrator. /usr/share/color is not suitable for machine
specific data, as this may be shared between different computers or
mounted read only.
