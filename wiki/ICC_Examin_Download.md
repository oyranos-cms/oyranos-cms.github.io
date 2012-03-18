---
title: ICC Examin/Download
permalink: wiki/ICC_Examin/Download/
layout: wiki
tags:
 - Oyranos
---

<h1>
[ICC Examin](http://www.oyranos.org/icc-examin)

</h1>
Stable Versions
---------------

ICC Examin is known to work on Linux, BSD, osX and Solaris. Windows will
currently not work.

### Sources

[Sources](http://sourceforge.net/projects/oyranos/files/ICC%20Examin/) @
SourceForge

[Elder
Downloads](http://www.behrmann.name/index.php?option=com_content&task=view&id=33)
are available from the behrmann site.

#### Dependencies

ICC Examin depends on following libraries and external applications:

-   FLTK version &lt;= 1.1.4 neede to build the GUI (needed by FLU as
    well). You may configure FLTK with several options enabled:

`   --enable-threads is needed for threads support (in ICC Examin)`  
`   --enable-xft is ok for antialiased fonts`  
`   --enable-debug is generally a good choice`  
`   --enable-shared is sometimes a good choice for smaller executables`

-   [Oyranos](/wiki/Oyranos/Download "wikilink") CMS
-   FTGL

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

#### Open Build Service

***[ICC
Examin](http://software.opensuse.org/download/package.iframe?project=multimedia:color_management&package=icc_examin)***

#### osX

[disk
image](http://sourceforge.net/projects/oyranos/files/ICC%20Examin/)
<http://www.behrmann.name/images/cms/dmg_64.png>

Development Versions
--------------------

[Git](/wiki/Oyranos/git "wikilink"): The actual development version can be
obtained through git. Instructions on how to obtain the code and how to
build, can be found on the Oyranos Wiki page
[Oyranos/git](/wiki/Oyranos/git "wikilink"). There is as well a build script
available for automated dependency checking, downloading and building.

[Snapshots and release
candidates](http://sourceforge.net/project/showfiles.php?group_id=177017)
are available from the SourceForge site. They are released non
regularily. The packages contain sources and all datas.

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
