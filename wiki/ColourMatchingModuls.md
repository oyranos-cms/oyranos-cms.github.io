---
title: ColourMatchingModuls
permalink: wiki/ColourMatchingModuls/
layout: wiki
tags:
 - Programms
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

License: 4 clause BSD [(not very handy for
distribution)](http://www.fsf.org/licensing/licenses/index_html#OriginalBSD)

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
    single pixel (for instance Brightness adjustement or desaturate).
    CTL is designed to be part of the Color Management process.
-   OpenShiva is inspired by Adobe's Hydra language from the AIF
    Toolkit, Shiva is a language that apply a kernel-like
    transformations on an image, that means it works using more than one
    pixel.

License: LGPL

Profiler
--------

#### ArgyllCMS

-   [ArgyllCMSGUI](http://www.digifab.com/ArgyllCMSGUI/) a GUI for some
    Argyll's command line tools
-   [CMS/ Argyll CMS](http://x3.ntf.uni-lj.si/~gojc/Argyll) a Argyll
    command line resampler
-   [dispcalGUI](http://hoech.net/dispcalGUI/) a display profiler
-   [Stefan's review](http://colorhacks.blogspot.com/) of ArgyllCMSGUI,
    “Argyll CMS” and dispcalGUI : \[09:57, 27 Aug 2008 (CEST)\]

License: GPL

#### LProf

[LProf](http://lprof.sourceforge.net/) a scanner and display profiler

License: GPL
