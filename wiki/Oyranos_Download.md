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

[Download](http://sourceforge.net/project/showfiles.php?group_id=177017&package_id=203716)
from the SourceForge site.

[Elder
Downloads](http://www.behrmann.name/index.php?option=com_content&task=view&id=34&Itemid=68)
are available from the behrmann site.

#### Dependencies

Oyranos depends on following libraries and external applications:

-   libxml2
-   FLTK version &lt;= 1.1.4 neede to build the GUI. You may configure
    FLTK with several options enabled:

`   --enable-threads is needed for threads support (in ICC Examin)`  
`   --enable-xft is ok for antialiased fonts`  
`   --enable-debug is generally a good choice`  
`   --enable-shared is sometimes a good choice for smaller executables`

-   Elektra, this is the configuration system used under linux.

Optionally:

-   [ICC Examin](/wiki/ICC_Examin/Download "wikilink") is the profile viewer
    of Oyranos' configuration GUI. It provides a view on profile
    internals and a gamut view. It uses littleCMS and Oyranos.
-   Xcalib for loading a given VideoCardGammaTag from profile to a
    running XFree86/Xorg session (optionally)
-   Cairo
-   Compiz
-   CUPS
-   libraw

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

<http://www.oyranos.org/images/fedora-logo.png>
[Fedora](https://admin.fedoraproject.org/pkgdb/acls/name/oyranos)

<http://www.oyranos.org/images/ubuntu_logo.png>
[Ubuntu](http://www.ubuntuupdates.org/oyranos)

#### openSUSE build server

***bekun*** OBS repositories for:

<http://www.oyranos.org/images/fedora-logo.png>  
\* 12

-   13

<http://www.oyranos.org/images/mandriva-logo-opt.png>  
\* 10

<http://www.oyranos.org/images/suse_logo.png>  
\* SLE\_11

-   11.1
-   11.2
-   11.3
-   Factory

***[openSUSE build server icc\_examin
search](http://software.opensuse.org/search?q=icc_examin&exclude_debug=true)***

***[home:bekun](http://download.opensuse.org/repositories/home:/bekun/)***
repository plain overview  

### Oyranos LiveCD

The Oyranos LiveCD is based on openSUSE and the preinstalled Oyranos
packages from home:bekun at OBS. It contains the nvidia binary graphics
drivers. Download from [suse
gallery](http://susegallery.com/a/8Kr6tw/oyranos).

Development Versions
--------------------

[Git](/wiki/Oyranos/git "wikilink"): The actual development version can be
obtained through git. Instructions on how to obtain the code and how to
build, can be found on the Oyranos Wiki page
[Oyranos/git](/wiki/Oyranos/git "wikilink"). There is as well a build script
available for automated dependency checking, downloading and building.

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
