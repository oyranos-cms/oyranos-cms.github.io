---
title: ColourMatchingModuls
permalink: wiki/ColourMatchingModuls/
layout: wiki
tags:
 - Programs
---

The CMM colormatching module is the “engine” for color conversions in
applications.

In Open Source applications, LittleCMS is the most used CMM. Other
widely used CMMs are the AppleCMM in MacOSX, the
[AdobeCMM](http://labs.adobe.com/downloads/cmm.html) and the CMM
delivered with Windows XP.

Open Source Implementations
---------------------------

#### Argyll

-   <http://www.argyllcms.com/>
-   Local, [Argyll Community
    Documentation](/wiki/Argyll_Community_Documentation "wikilink")

License: GPL, with an exception to libicc and libcgats

#### LittleCMS

-   <http://www.littlecms.com/>

License: MIT

#### SampleICC

-   <http://sampleicc.sourceforge.net/> — The ICC's official sample
    implementation.

License: newBSD (3 clauses)

#### QCMS

-   Mozillas implementation of a CMM:
    <http://muizelaar.blogspot.com/2009/06/qcms-color-management-for-web.html>
-   code: <git://git.freedesktop.org/~jrmuizel/qcms>

#### GCMS

-   an historical CMM effort: <http://www.gcms.coloraid.de/>

#### CTL

-   <http://sourceforge.net/projects/ampasctl> - Ilm's effort to handle
    floating point colours precisely and according to the needs in the
    [film industry](http://www.oscars.org/council/ctl.html).

License: [modified](http://savannah.gnu.org/task/?6171) [new
BSD](http://www.opensource.org/licenses/bsd-license.php) (? with
jurisdiction to California) ...

#### OpenGTL

-   <http://opengtl.org/> - The G of GTL means either Graphics or
    Generics, the T means Transformation and the L means Libraries or
    Languages. The C++ libraries are created by Cyrille Berger.

Currently the focus is on developing two languages, designed for two
different implementations.

-   OpenCTL which is a GPL compatible of the Color Transformation
    Language, this language is dedicated at transforming the value of a
    single pixel (for instance Brightness adjustment or desaturate). CTL
    is designed to be part of the Color Management process.
-   OpenShiva is inspired by Adobe's Hydra language from the AIF
    Toolkit, Shiva is a language that apply a kernel-like
    transformations on an image, that means it works using more than one
    pixel.

License: LGPL

-   [A simple video tutorial on how to use PixelBender alias
    Hydra](http://www.gotoandlearn.com/play?id=83) from Lee Brimelow

Profiler
--------

#### ArgyllCMS

-   [dispcalGUI](http://hoech.net/dispcalGUI/) a display profiler
-   [Stefan's review](http://colorhacks.blogspot.com/) of ArgyllCMSGUI,
    “Argyll CMS” and dispcalGUI : \[09:57, 27 Aug 2008 (CEST)\]
-   [Gnome Color Manager](http://live.gnome.org/GnomeColorManager) is a
    CMS, but as well a front end to the ArgyllCMS profiler

#### LProf

[LProf](http://lprof.sourceforge.net/) a scanner and display profiler

License: GPL

Tools
-----

#### ArgyllCMS

-   [ImgTarget](http://www.blackfiveimaging.co.uk/index.php?article=02Software%2F02ImgTarget)
    resembles a intelligent CMM in a GUI
-   [ArgyllCMSGUI](http://www.digifab.com/ArgyllCMSGUI/) a GUI for some
    Argyll's command line tools
-   [Argyll CMS](http://x3.ntf.uni-lj.si/~gojc/ArgyllCMS_GUI/) a Argyll
    command line resampler
-   [Stefan's review](http://colorhacks.blogspot.com/) of ArgyllCMSGUI,
    “Argyll CMS” and dispcalGUI : \[09:57, 27 Aug 2008 (CEST)\]
-   [GaMapICC](http://digitalproof.info/gamapicc/) is a Mac OS X
    droplet, which works like a intelligent CMM

#### SampleICC

-   [IccXML](http://iccxml.sf.net) a ICC &lt;-&gt; XML serialiser

