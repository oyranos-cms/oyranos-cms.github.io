---
title: Ghostscript
permalink: wiki/Ghostscript/
layout: wiki
tags:
 - Programms
---

Features
--------

-   colour management through the Postscript language with CRD's and
    CDA's
-   convert complex colour documents to flat representations, e.g. Tiff,
    PNG

Investigation
-------------

Create a CRD with relative colorimetric rendering intent:

` `[`icc2ps`](http://www.littlecms.com/)` -o /opt/local/share/color/icc/ISOuncoatedyellowish.icc -t 1 > myCMYKCRD.ps`

Activate the CRD into the myCMYKCRD.ps resource file:

` echo `“`/Current`` ``/ColorRendering`` ``findresource`` ``setcolorrendering`”` >> myCMYKCRD.ps`

Call Ghostscipt to convert the document:

` gs -sDEVICE=tiff32nc -o MyOutputFile.tiff -f myCMYKCRD.ps FileToProcess.pdf`

Use -dUseCIEColor if you want to touch the Cmyk colours. Otherwise leave
it as is.

Embedd the profile:

` tifficc -e -i ISOuncoatedyellowish.icc -o ISOuncoatedyellowish.icc MyOutputFile.tiff MyOutputFile_icc.tiff`

Probably use the -w option to preserve 16-bit images.

The above approach is dependent on Ghostscript's Postscript interpreter.
It uses internally CIEXYZ as PCS. There are clear issues, when it comes
to bigger gamut differences. Thus it is not useable to convert to big
gamut devices such as the K3 ink jets and other photo printers.

Links
-----

-   Mainsite: [www.ghostscript.com](http://www.ghostscript.com)
-   news thread about [Ghostscript colour
    management](http://newsgroups.derkeiler.com/Archive/Comp/comp.lang.postscript/2007-08/msg00019.html)
    with Gerhard Fuernkranz
-   Marti Maria about
    [icc2ps](http://sourceforge.net/mailarchive/forum.php?thread_name=00004456.3EBBBE6F%40david.englram.de&forum_name=lcms-user)
-   [PLRM](http://www.adobe.com/products/postscript/pdfs/PLRM.pdf)
    Postscript Language Reference from Adobe - chapter 7 Rendering
-   [a short
    statement](http://www.ghostscript.com/pipermail/gs-devel/2008-August/007871.html)
    about future CM in Ghostscript

[back -&gt; Applications](/wiki/Applications "wikilink")  
[back -&gt; Device Settings](/wiki/Device_Settings "wikilink")
