---
title: Ghostscript
permalink: wiki/Ghostscript/
layout: wiki
tags:
 - Programms
---

Features
--------

-   colour management over the Postscript language with CRD's and CDA's
-   PDF colour management
-   convert complex colour documents to flat representations, e.g. Tiff,
    PNG

Investigation
-------------

` gs -sDEVICE=tiff32nc -o MyOutputFile.tiff -f myCMYKCRD.ps FileToProcess.pdf`

where myCMYKCRD.ps is to be created with for instance
[lcms's](http://www.littlecms.com/) icc2ps tool. It should contain a
CRD.

Links
-----

-   Mainsite: [www.ghostscript.com](http://www.ghostscript.com)
-   news thread about [Ghostscript colour
    management](http://newsgroups.derkeiler.com/Archive/Comp/comp.lang.postscript/2007-08/msg00019.html)

[back -&gt; Applications](/wiki/Applications "wikilink")
