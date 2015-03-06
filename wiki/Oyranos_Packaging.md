---
title: Oyranos/Packaging
permalink: wiki/Oyranos/Packaging/
layout: wiki
tags:
 - Oyranos
---

Dependencies
------------

For the development version check out
[Oyranos/git](/wiki/Oyranos/git "wikilink") build and install.

Additional you'd need FLTK and possibly xcalib. These dependencies are
mentioned here: [Oyranos/Download](/wiki/Oyranos/Download "wikilink")

Packaging
---------

### Bundling

Oyranos has currently no osX Framework or bundling support in its make
files. Eighter use the ICC Examin bundle and look there at profiles and
the files with 'oyranos' in their name.

Or you can copy a complete installation into the bundle. The later is
support by the following target in Oyranos:

`make DESTDIR=`“`/my/home/bundle.app/Contents/Resources/`”` install`

You have to set the XDG veriables and others to match the paths relative
to the bundle to allow Oyranos to locate various data in a bundle.

Again look at the ICC Examin bundle as an example: ICC
Examin.app/Contents/MacOS/ICC Examin .

Take the lastest ICC Examin bundle, the folder ending with app, similiar
named to
[icc\_examin-x.xx\_rcx.app.tgz](http://sourceforge.net/project/showfiles.php?group_id=177017&package_id=247749&release_id=543945).

A additional hint is to copy libelektra-filesys and libltdl into your
bundle to satisfy Elektra. It will fix some warnings.

References
----------

-   [inline PACKAGING
    file](https://github.com/oyranos-cms/oyranos/blob/master/PACKAGING.md)

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
