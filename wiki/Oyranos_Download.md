---
title: Oyranos/Download
permalink: wiki/Oyranos/Download/
layout: wiki
tags:
 - Oyranos
---

<h1>
[Oyranos](/wiki/Oyranos "wikilink")

</h1>
Stable Versions
---------------

Oyranos is known to work on Linux, BSD, osX and Solaris. Windows will
currently not work.

### Sources

[Download](http://sourceforge.net/projects/oyranos/files/) from the
SourceForge site.

[Elder
Downloads](http://www.behrmann.name/index.php?option=com_content&task=view&id=34&Itemid=68)
are available from the behrmann site.

#### Dependencies

Oyranos depends on following libraries and external applications:
Mandatory:

-   libxml2
-   libXcm - for X11 and Quarz monitor support
-   libXinerama, libXrandr, libXfixes and libXxf86vm for X11 support
-   lcms2 - for colour conversions

Optionally:

-   FLTK version &lt;= 1.1.4 neede to build the GUI. You may configure
    FLTK with several options enabled:

`   --enable-threads is needed for threads support (in ICC Examin)`  
`   --enable-xft is ok for antialiased fonts`  
`   --enable-debug is generally a good choice`  
`   --enable-shared is sometimes a good choice for smaller executables`

-   Qt - for a nice observer utility
-   Elektra, this is the configuration system used under linux.
-   yajl, a JSON parser library
-   [ICC Examin](/wiki/ICC_Examin/Download "wikilink") is the profile viewer
    of Oyranos' configuration GUI. It provides a view on profile
    internals and a gamut view. It uses littleCMS and Oyranos.
-   Xcalib for loading a given VideoCardGammaTag from profile to a
    running XFree86/Xorg session (optionally)
-   CUPS - for CUPS ICC configuration support
-   libraw - for cameraRAW decoding
-   SANE - only with Oyranos SANE\_CAP\_COLOUR patch
-   Cairo - for a example

#### Compile Instructions

For building unpack the tgz file and type \#configure; make; make
install. Optionally you can specifiy an other than the default prefix
/opt/local by typing:

`   configure --prefix=/what/you/like`  
`   make`  
`   make install       # (optionally)`

`   configure --help   # will show details`  
`   make help          # shows the available targets`

Detailed build instructions are as well included in the packages.

### Binary Packages

#### Distribution packages

<http://www.oyranos.org/images/archlogo.png>
[ArchLinux](https://aur.archlinux.org/packages.php?O=0&K=oyranos&do_Search=Go)

<http://www.oyranos.org/images/fedora-logo.png>
[Fedora](https://admin.fedoraproject.org/pkgdb/acls/name/oyranos)

<http://www.oyranos.org/images/suse_logo.png>
[openSUSE](http://software.opensuse.org/search?q=oyranos)

[Slackware](http://slackbuilds.org/result/?search=oyranos)

<http://www.oyranos.org/images/ubuntu_logo.png>
[Ubuntu](http://www.ubuntuupdates.org/oyranos)

#### Open Build Service

***[Oyranos](http://software.opensuse.org/download/package.iframe?project=multimedia:color_management&package=oyranos)***  

### Oyranos LiveCD

The [Oyranos
LiveCD](http://sourceforge.net/projects/openicc/files/Demo/) is based on
openSUSE and the preinstalled Oyranos packages from
multimedia:color\_management at OBS. The project page is at [suse
gallery](http://susestudio.com/a/8Kr6tw/oyranos-multimedia-121).

Development Versions
--------------------

[Git](/wiki/Oyranos/git "wikilink"): The actual development version can be
obtained through git. Instructions on how to obtain the code and how to
build, can be found on the Oyranos Wiki page
[Oyranos/git](/wiki/Oyranos/git "wikilink"). There is as well a build script
available for automated dependency checking, downloading and building.

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
