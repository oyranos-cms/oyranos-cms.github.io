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
-   FLTK version &lt;= 1.1.4 neede to build the GUI (needed by FLU as
    well). You may configure FLTK with several options enabled:

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

<http://www.oyranos.org/images/fedora-logo.png>
[Fedora](https://admin.fedoraproject.org/pkgdb/acls/name/oyranos)

#### openSUSE build server

***bekun*** YUM repositories for:

<http://www.oyranos.org/images/fedora-logo.png>  
[f-10](https://www.oyranos.org/wiki/images/b/b0/Bekun-Fedora_10.rpm)

-   12
-   13

<http://www.oyranos.org/images/suse_logo.png>  
[openSUSE-10.3](https://www.oyranos.org/wiki/images/a/a7/Bekun-openSUSE_10.3.rpm)
[openSUSE-11.0](https://www.oyranos.org/wiki/images/0/02/Bekun-openSUSE_11.0.rpm)

-   11.2

After installing one of the above setup RPM's the ***bekun*** repository
is activated in yum. For a full installation install the icc\_examin
package:

`yum install icc_examin`

Yum should resolve all dependcies. The *icc\_examin-cinepaint* package
is for a more indepth colour space exploration inside
[CinéPaint](/wiki/CinePaint "wikilink").

In case a missed libelektra.so.2 message is shown, as can happen on
Fedora, try first the following command:

`yum erase elektra`

and repeat the above *icc\_examin* or *icc\_examin-cinepaint*
installation.

***bekun*** repository plain overview:  
[bekun](http://download.opensuse.org/repositories/home:/bekun/)
supported are Fedora, openSUSE and to some extent Mandriva.

Development Versions
--------------------

[Git](/wiki/Oyranos/git "wikilink"): The actual development version can be
obtained through git. Instructions on how to obtain the code and how to
build, can be found on the Oyranos Wiki page
[Oyranos/git](/wiki/Oyranos/git "wikilink"). There is as well a build script
available for automated dependency checking, downloading and building.

[Snapshots and release
candidates](https://sourceforge.net/project/showfiles.php?group_id=177017)
are available from the SourceForge site. They are released non
regularily. The packages contain sources and all datas.

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
